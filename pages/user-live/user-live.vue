<template>
	<view>
		<view v-for="(item,index) in mainData" :key="index">
			<view class="p-3 pb-2 color2 line-h">
				<view class="font-40 font-w pb-4">{{Utils.substr(item.menu,0,4)}}年</view>
				<view class="font-26 fontw-600"><text class="font-42 font-w">{{Utils.substr(item.menu,5,10)}}</text></view>
			</view>
			<view class="text-center pb-4">
				<view class="color6 f5bj d-flex proHead">
					<view class="bb">商品名称</view>
					<view class="bb">商品ID</view>
				</view>
				<view class="d-flex pro" v-for="(c_item,c_index) in item.data" :key="c_index">
					<view class="bb">
						<view class="avoidOverflow2">{{c_item.passage_array.skuName?c_item.passage_array.skuName:''}}</view>
					</view>
					<view class="bb d-flex a-center j-center">
						<view class="avoidOverflow2">{{c_item.relation_user?c_item.relation_user:''}}</view>
					</view>
				</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				searchItem:{},
				Utils:this.$Utils
			}
		},
		
		onLoad(options) {
			const self = this;
			self.searchItem.user_no = uni.getStorageSync('user_info').user_no;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				//postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				const callback = (res) => {
					if (res.info.data.length > 0) {
						for (var i = 0; i < res.info.data.length; i++) {
							res.info.data[i].create_time = res.info.data[i].create_time.substr(0,10)
							if(self.mainData.length>0){
								var hasone = false;
								for(var j =0;j<self.mainData.length;j++){
									if(res.info.data[i].create_time==self.mainData[j].menu){
										self.mainData[j].data.push(res.info.data[i]);
										hasone = true;
									};
								};
								if(!hasone){
									self.mainData.push({
										menu: res.info.data[i].create_time,
										data:[res.info.data[i]]
									});
								};
							}else{
								self.mainData.push({
									menu: res.info.data[i].create_time,
									data:[res.info.data[i]]
								})
							};
						};
						console.log(self.mainData)
						
						//self.mainData.push.apply(self.mainData,res.info.data)
					}
					console.log('self.mainData',self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.messageGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.fontw-600{font-weight: 600;}
</style>
