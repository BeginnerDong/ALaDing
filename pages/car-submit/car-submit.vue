<template>
	<view>
		<image src="../../static/images/icon02.png" class="d-icon"></image>
		<view class="font-30 color2 text-center font-w mb-5">数据提交成功</view>
		
		<view class="mt-3 text-center">
			<view class="color6 f5bj d-flex proHead">
				<view class="bb">商品名称</view>
				<view class="bb">商品ID</view>
			</view>
			<view class="d-flex pro" v-for="(item,index) in mainData" :key="index">
				<view class="bb">
					<view class="avoidOverflow2">{{item.passage_array.skuName?item.passage_array.skuName:''}}</view>
				</view>
				<view class="bb d-flex a-center j-center">
					<view class="avoidOverflow2">{{item.relation_user?item.relation_user:''}}</view>
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
				searchItem:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.searchItem.id = ['in',uni.getStorageSync('ids')];
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
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					};
					console.log('self.mainData',self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.messageGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.d-icon{width: 141rpx;height: 135rpx;margin: 60rpx auto 40rpx;}
</style>
