<template>
	<view class="user" v-if="showAll">
		<view class="head line-h">
			<view class="userCon px-3 py-3 d-flex a-center">
				<image style="border-radius: 50%;overflow: hidden;" :src="userData.headImgUrl!=''?userData.headImgUrl:''" mode=""></image>
				<view class="colorf ml-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="pr-1 font-30">{{userData.nickname?userData.nickname:''}}</view>
						<view class="sign1">{{userData.behavior==0?'游客':(userData.behavior==1?'主播':'导师')}}</view>
					</view>
					<view class="d-flex a-center" v-if="userData.behavior>0">
						<view class="pr-1 font-26">邀请码：{{userData.user_no?userData.user_no:''}}</view>
						<view class="sign1" @click="getClipboardData">复制</view>
					</view>
				</view>
				<image src="../../static/images/user-icon.png" style="width: 42rpx;height: 39rpx;" @click="Router.navigateTo({route:{path:'/pages/user-Information/user-Information'}})"></image>
			</view>
			<view class="font-50 colorf font-w text-center pt-3 pb-2">{{userData.info?userData.info.balance:''}}</view>
			<view class="font-22 text-center colorf pb-3">可提现金额(￥)</view>
			<view class="d-flex j-center pb-4">
				<view class="btn1" @click="Router.navigateTo({route:{path:'/pages/user-Withdrawal/user-Withdrawal'}})">申请提现</view>
				<view class="btn1" @click="Router.navigateTo({route:{path:'/pages/user-WithdrawalRecord/user-WithdrawalRecord'}})">提现记录</view>
			</view>
		</view>
		
		<view class="userBox1 line-h text-center bg-white rounded10 d-flex mx-3">
			<view class="px-3 d-flex flex-column a-center j-center userBox1L">
				<view class="font-22 color2" style="padding-bottom: 25rpx;">本月平台奖励</view>
				<view class="font-30 color2">{{userData.FlowLog.count?userData.FlowLog.count:0}}</view>
			</view>
			<view class="flex-1">
				<view class="font-24 color2 py-3">推广佣金</view>
				<view class="d-flex">
					<view class="item">
						<view class="font-22 color9">本月预估结算金额</view>
						<view class="font-30 color2 py-2">暂无数据</view>
						<view class="font-22 color2 pb-3">已结算账单金额</view>
					</view>
					<view class="item">
						<view class="font-22 color9">下月预估结算金额</view>
						<view class="font-30 color2 py-2">暂无数据</view>
						<view class="font-22 color2 pb-3 djs">待结算</view>
					</view>
				</view>
			</view>
		</view>

		<view class="userBox2 bg-white mx-3 mt-2 rounded10">
			<view class="font-28 font-w mx-3 py-3 borderB-f5">常用工具</view>
			<view class="itemBox d-flex flex-wrap pb-4">
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-team/user-team'}})">
					<image src="../../static/images/about-icon.png" mode=""></image>
					<view>我的团队</view>
				</view>
				<view class="item" v-if="userData.behavior>0" @click="Router.navigateTo({route:{path:'/pages/user-promotion/user-promotion'}})">
					<image src="../../static/images/about-icon1.png" mode=""></image>
					<view>推广中心</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-profit/user-profit'}})">
					<image src="../../static/images/about-icon2.png" mode=""></image>
					<view>我的收益</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-aboutUs/user-aboutUs'}})">
					<image src="../../static/images/about-icon3.png" mode=""></image>
					<view>关于我们</view>
				</view>
				<button class="item" v-if="userData.behavior==1"  @click="Router.navigateTo({route:{path:'/pages/identityInformation/identityInformation'}})">
					<image src="../../static/images/about-icon5.png" mode=""></image>
					<view>身份信息</view>
				</button>
				<button class="item"  @click="Router.navigateTo({route:{path:'/pages/user-quanyi/user-quanyi'}})">
					<image src="../../static/images/about-icon6.png" mode=""></image>
					<view>我的权益</view>
				</button>
				<button class="item" open-type="contact">
					<image src="../../static/images/about-icon4.png" mode=""></image>
					<view>专属客服</view>
				</button>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-live/user-live'}})">
					<image src="../../static/images/icon01.png" mode=""></image>
					<view>直播推广</view>
				</view>
				
				
			</view>
		</view>

		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item"  @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/course/course'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item .on">
				<image src="../../static/images/nabar5-a.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				userData: {},
				showAll:false,
				isIphoneX:false
			}
		},

		onLoad() {
			const self = this;
			self.isIphoneX = wx.getStorageSync('isIphoneX');
			self.$Utils.loadAll(['getUserData'], self);
		},


		methods: {
			
			showToast(){
				const self = this;
				uni.showModal({
					title:'',
					content:'功能开发中~',
					showCancel:false
				})
			},
			
			getClipboardData(){
				const self = this;
				uni.setClipboardData({
				    data: self.userData.user_no,
				    success: function () {
				        console.log('success');
				    }
				});
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
							type:2,
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
									type:2,
									create_time: ['between', [monthStart, nowTime]]
								}
							],
						},
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
						if(self.userData.parent_no==''){
							// self.Router.redirectTo({route:{path:'/pages/invitation-code/invitation-code'}})
							self.showAll = true
						}else{
							self.showAll = true
						}
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			addFlowLog() {
				const self = this;
				const postData = {};
				/* if(uni.getStorageSync('user_info').thirdApp.yuanbao<=parseFloat(self.userInfoData.yb_today)){
					return
				}; */
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					type: 3,
					count: 1000,
					trade_info: '',
					account: 1,
					thirdapp_id: 2,
					user_no: uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						
					}
				};
				self.$apis.flowLogAdd(postData, callback);
			},
		}
	}
</script>

<style>
	page {
		background-color: #F5F5F5;
	}

	.head {
		background-color: #FF7B8E;
		padding-bottom: 100rpx;
	}

	.userCon image {
		height: 120rpx;
		width: 120rpx;
	}

	.userBox1 {
		margin-top: -100rpx;
	}

	.userBox1L {
		border-right: 1px dashed #d5d5d5;
	}

	.userBox1 .item {
		width: 50%;
	}

	.djs {
		color: #F51E1E;
	}


	.itemBox .item {
		display: flex;
		align-items: center;
		width: 25%;
		flex-direction: column;
		font-size: 22rpx;
		color: #222;
	}

	.itemBox .item image {
		width: 52rpx;
		height: 46rpx;
		margin: 40rpx 0 20rpx;
	}
	
	.itemBox .item:last-child image{
		width: 45rpx;
	}

	button {
		background: none;
		line-height: 1.5;
		margin-left: 0;
		margin-right: 0;
		font-size: 14px;
		border-radius: 0;
	}

	button::after {
		border: none;
	}

	.button-hover {
		color: #000000;
		background: none;
	}
	.user{padding-bottom: 150rpx;}
</style>
