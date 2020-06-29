<template>
	<view>
		<view class="px-3 bg-white">
			<view class="line-h font-28 color2 d-flex j-sb a-center borderB-f5" v-for="item of mainData" :key="item.id">
				<view>
					<view class="py-3">{{item.trade_info}}</view>
					<view class="color6 pb-3">{{item.create_time}}</view>
				</view>
				<view>{{item.count}}</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				searchItem:{
					type:2,
					thirdapp_id:2,
					withdraw:1
				},
				mainData:[],
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self)
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
					};
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.tokenFuncName = 'getProjectToken'
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.flowLogGet(postData, callback);
			},
		},
		
	};
</script>

<style>
page{background-color: #f5f5f5;}
</style>
