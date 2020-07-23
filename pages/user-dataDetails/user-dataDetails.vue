<template>
	<view>
		<view class="table">
			<view class="tr">
				<view class="th">日期</view>
				<view class="th">订单量</view>
				<view class="th">获得佣金</view>
				<view class="th">平台奖励</view>
			</view>
			<view class="tr" v-for="item of mainData" :key="item.id" v-if="mainData.length>0">
				<view class="td">{{item.create_time}}</view>
				<view class="td">{{item.order}}</view>
				<view class="td">{{item.balance}}</view>
				<view class="td">{{item.reward}}</view>
			</view>
			<view style="font-weight: 700;width: 100%;text-align: center;" class="item  a-center py-3 borderB-f5" v-if="mainData.length==0">
				暂无数据
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				
				mainData:[],
			}
		},
		
		onLoad(options) {
			const self = this;
			self.user_no = options.user_no;
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
				postData.searchItem = {
					user_no:self.user_no,
					user_type:0
				};
				postData.tokenFuncName = 'getProjectToken'
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.statisticsGet(postData, callback);
			},
		},
		
	};
</script>

<style>
page{background-color: #f5f5f5;}
.table{width: 100%;background-color: #fff;color: #222;}
.tr{display: flex;text-align: center;width: 100%;}
.th,.td{width: 25%;box-sizing: border-box;border-right: 1px solid #E1E1E1;height: 88rpx;line-height: 88rpx;}
.th:nth-child(4),.td:nth-child(4){border-right: none;}
.th{background-color: #fff2f4;font-size: 28rpx;}
.td{border-bottom: 1px solid #E1E1E1;font-size: 26rpx;}
</style>
