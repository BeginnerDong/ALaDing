<template>
	<view :style="isIphoneX?'padding-bottom: 60rpx':''">
		<view class="bg-white p-3 mx-3 my-2 position-relative rounded10 overflow-h">
			<view class="flex1">
				<input type="text" value="" placeholder="姓名" />
				<input type="text" value="" placeholder="电话" />
			</view>
			<image src="../../static/images/line.png" class="line"></image>
		</view>
		
		<view class="item d-flex mx-3 px-3 py-3 bg-white rounded10 mt-3">
			<image :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image>
			<view class="d-flex flex-column j-sb px-2 flex-1">
				<view class="font-28 color2 font-w">{{mainData.title?mainData.title:''}}</view>
				<view class="d-flex a-center line-h ">
					<view class="price font-34 pr-2">{{mainData.price?mainData.price:''}}</view>
					<view class="sign flex">
						<view>{{mainData.behavior==1?'主播':'导师'}}</view>
						<image src="../../static/images/start.png" class="wh20"></image>
					</view>
				</view>
			</view>
		</view>
		
		<view class="d-flex j-sb bg-white position-fixed bottom-0 left-0 right-0 courseFoot" :style="isIphoneX?'padding-bottom: 60rpx':''">
			<view class="px-3 d-flex a-center">
				合计<view class="price font-34 pr-2 pl-2">{{mainData.price}}</view>
			</view>
			<button class="submitBtn colorf font-30 text-center"  style="border-radius: 0;"
			open-type="getUserInfo"  @getuserinfo="Utils.stopMultiClick(submit)">确认订单</button>
		</view>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				mainData:{},
				distriData:[],
				isIphoneX:false
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.isIphoneX = wx.getStorageSync('isIphoneX');
			self.$Utils.loadAll(['getMainData','getDistriData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2,
					id:self.id
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getDistriData() {
				const self = this;
				const postData = {
					searchItem:{thirdapp_id:2,child_no:uni.getStorageSync('user_info').user_no}
				};
				postData.tokenFuncName = 'getProjectToken'
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.distriData.push.apply(self.distriData,res.info.data)
					}
					self.$Utils.finishFunc('getDistriData');
				};
				self.$apis.distriGet(postData, callback);
			},
			
			submit(){
				const self = this;
				uni.setStorageSync('canClick', false);
				var orderList = []
				orderList.push({product_id:self.mainData.id,count:1,type:1})
				const callback = (user, res) => {
					self.addOrder(orderList)
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			addOrder(orderList) {
				const self = this;	
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.tokenFuncName = 'getProjectToken';
				console.log('addOrder',postData);
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = {	
					wxPay:{
						price:parseFloat(self.mainData.price)
					}
				};	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [];
				postData.payAfter.push({
					tableName: 'User',
					FuncName: 'update',
					data: {
						behavior:self.mainData.behavior
					},
					searchItem:{
						user_no:uni.getStorageSync('user_info').user_no
					}
				});
				if (self.distriData.length > 0) {
					for (var i = 0; i < self.distriData.length; i++) {
						if (self.distriData[i].level == 1) {
							postData.payAfter.push({
								tableName: 'FlowLog',
								FuncName: 'add',
								data: {
									count: parseFloat(self.mainData.class_one),
									thirdapp_id: 2,
									status: 1,
									trade_info: '平台奖励',
									type: 2,
									account: 1,
									user_no: self.distriData[i].parent_no,
									relation_user: uni.getStorageSync('user_info').user_no,
								},
							}, )
						} else if (self.distriData[i].level == 2) {
							postData.payAfter.push({
								tableName: 'FlowLog',
								FuncName: 'add',
								data: {
									count: parseFloat(self.mainData.class_two),
									thirdapp_id: 2,
									status: 1,
									trade_info: '平台奖励',
									type: 2,
									account: 1,
									user_no: self.distriData[i].parent_no,
									relation_user: uni.getStorageSync('user_info').user_no
								},
							}, )
						}
					}
				}
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 1000,
										success: function() {
											
										}
									});
									setTimeout(function() {
										self.$Router.redirectTo({route:{path:'/pages/user/user'}})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									uni.showToast({
										title: '支付失败',
										duration: 2000
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '支付成功',
								duration: 1000,
								success: function() {
									
								}
							});
							setTimeout(function() {
								self.$Router.redirectTo({route:{path:'/pages/user/user'}})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
</style>
<style scoped>
.item image{width: 180rpx;height: 180rpx;border-radius: 10rpx;}
.courseFoot{}
.submitBtn{height: 100rpx;width: 280rpx;background-color: #FF7B8E;line-height: 100rpx;}
.wh20{width: 20rpx!important;height: 20rpx!important;margin-left: 5rpx;}
.sign{width: auto;padding: 0 5rpx;}
input{width: 300rpx;height: 67rpx;font-size: 24rpx;border: 1px solid #e1e1e1;border-radius: 10rpx;text-align: center;}
.line{width: 690rpx;height: 4rpx;position: absolute;bottom: 0;left: 0;}
</style>
