<template>
	<view class="profit line-h">
		<view class="head">
			<view class="font-50 colorf font-w text-center pt-3 pb-2">{{canWithdraw?canWithdraw:'0.00'}}</view>
			<view class="font-22 text-center colorf pb-5">可提现金额(￥)</view>
		</view>
		<view class="proBox1 d-flex a-center j-sb rounded10 bg-white mx-3 shadow">
			<view class="item">
				<view class="font-30 color6 py-2">{{userData.FlowLog.count?userData.FlowLog.count:0}}</view>
				<view class="font-22 color6 pb-3">本月平台奖励</view>
			</view>
			<!-- <view class="item">
				<view class="font-30 color6 py-2">暂无数据</view>
				<view class="font-22 color6 pb-3">本月推广佣金</view>
			</view> -->
			<view class="item">
				<view class="btn2" @click="Router.navigateTo({route:{path:'/pages/user-Withdrawal/user-Withdrawal'}})">申请提现</view>
			</view>
		</view>

		<view class="d-flex j-sa borderB-f5 text-center proList">
			<view class="font-28 color2 proLi" :class="proLiCurrent==1?'on':''" @click="changeLi(1)">全部收益</view>
			<view class="font-28 color2 proLi" :class="proLiCurrent==2?'on':''" @click="changeLi(2)">推广收益</view>
			<view class="font-28 color2 proLi" :class="proLiCurrent==3?'on':''" @click="changeLi(3)">平台奖励</view>
		</view>

		<view class="proBox2 px-3">
			<view class="item d-flex a-center py-3 borderB-f5" 
				v-for="item of mainData" 
				:key="item.id"
			>
				<image style="border-radius: 50%;overflow: hidden;" :src="item.relationUser&&item.relationUser[0]?item.relationUser[0].headImgUrl:''" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">{{item.relationUser&&item.relationUser[0]?item.relationUser[0].nickname:''}}</view>
						<!-- <view class="sign2" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==2">导师</view>
						<view class="sign3" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==1">主播</view> -->
						
					</view>
					<view class="color6">{{item.trade_info}}</view>
				</view>
				<view class="font-26 color2 djs" style="flex:1;text-align: right;">{{item.count}}</view>
			</view>
		</view>
		<view class="proBox2 px-3"  v-if="mainData.length==0">
			<view style="font-weight: 700;width: 100%;text-align: center;margin-top: 200rpx;">暂无数据</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				proLiCurrent: 1,
				userData: {},
				mainData: [],
				searchItem: {
					thirdapp_id: 2,
					type: 2,
					count: ['>', 0],
					isPush:['in',[1,2]],
					status:1
				},
				canWithdraw:0
			}
		},

		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.canWithdraw = uni.getStorageSync('canWithdraw');
			self.$Utils.loadAll(['getUserData', 'getMainData'], self);
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
				postData.getAfter = {
					relationUser: {
						tableName: 'User',
						middleKey: 'relation_user',
						key: 'user_no',
						searchItem: {
							status: 1
						},
						condition: '='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.flowLogGet(postData, callback);
			},

			changeLi(i) {
				const self = this;
				if(self.proLiCurrent!=i){
					self.proLiCurrent = i;
					if(self.proLiCurrent==1){
						self.searchItem.isPush = ['in',[1,2]]
					}else if(self.proLiCurrent==2){
						self.searchItem.isPush = 2
					}else if(self.proLiCurrent==3){
						self.searchItem.isPush = 1
					};
					self.getMainData(true)
				}
			},

			getUserData() {
				const self = this;
				const postData = {};
				var data = new Date(); //本月
				data.setDate(1);
				data.setHours(0);
				data.setSeconds(0);
				data.setMinutes(0);
				var monthStart = parseInt(data.getTime() / 1000);
				var nowTime = Date.parse(new Date()) / 1000;
				postData.tokenFuncName = 'getProjectToken';
				postData.getAfter = {
					FlowLog: {
						tableName: 'FlowLog',
						middleKey: 'user_no',
						key: 'user_no',
						searchItem: {
							status: 1,
							count: ['>', 0],
							type: 2,
							isPush:1,
							create_time: ['between', [monthStart, nowTime]]
						},
						condition: '=',
						compute: {
							count: [
								'sum',
								'count',
								{
									status: 1,
									count: ['>', 0],
									type: 2,
									isPush:1,
									create_time: ['between', [monthStart, nowTime]]
								}
							],
						},
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
		}
	}
</script>

<style>
	.profit .head {
		background-color: #FF7B8E;
		padding-bottom: 70rpx;
	}

	.proBox1 {
		margin-top: -70rpx;
	}

	.proBox1 .item {
		width: 50%;
		text-align: center;
		position: relative;
	}

	.proBox1 .item::before {
		content: '';
		height: 50rpx;
		border-left: 1px dashed #d5d5d5;
		position: absolute;
		right: 0;
		top: 50%;
		margin-top: -25rpx;
	}

	.proBox1 .item:nth-child(3)::before {
		border-left: none;
	}

	.btn2 {
		margin: 0 auto;
	}

	.proLi {
		padding: 40rpx 0 30rpx;
		width: 33.33%;
	}

	.proList .on {
		color: #FF7B8E;
		font-weight: 700;
		position: relative;
	}

	.proList .on::before {
		content: '';
		width: 30rpx;
		height: 4rpx;
		background-color: #FF7B8E;
		position: absolute;
		bottom: 0;
		left: 50%;
		margin-left: -15rpx;
	}

	.proBox2 image {
		width: 100rpx;
		height: 100rpx;
	}

	.djs {
		color: #F51E1E;
	}
</style>
