<template>
	<view v-if="showAll">
		<view class="courseBox">
			<view class="mx-3 rounded10 shadow-sm mt-2 course-item" v-for="(item,index) of mainData" :key="item.id" :data-id="item.id"
			 @click="Router.navigateTo({route:{path:'/pages/courseDetails/courseDetails?id='+$event.currentTarget.dataset.id}})">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
				<view class="px-2 line-h">
					<view class="py-3 font-30 color2">{{item.title}}</view>
					<view class="d-flex a-center pb-3">
						<view class="price font-34 pr-1">{{item.price}}</view>
						<view class="sign flex">
							<view>{{item.behavior==1?'主播':'导师'}}</view>
							<image src="../../static/images/start.png" class="wh20"></image>
						</view>
					</view>
				</view>
			</view>
		</view>



		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item" @click="showToast">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item .on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item" @click="showToast">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/login/login'}})">
				<image src="../../static/images/nabar5.png" mode=""></image>
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
				mainData: [],
				showAll: false,
				isIphoneX:false
			}
		},

		onLoad() {
			const self = this;
			//let modelmes = wx.getStorageSync('modelmes');
			self.isIphoneX = wx.getStorageSync('isIphoneX');
			
			self.$Utils.loadAll(['getMainData', 'getUserData'], self);
		},

		methods: {


			tokenGet() {
				const self = this;
				const postData = {
					searchItem: {
						user_no: 'U706206460389216'
					}
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.userData = res.info;
						if (self.userData.parent_no == '') {
							self.Router.redirectTo({
								route: {
									path: '/pages/invitation-code/invitation-code'
								}
							})
						} else {
							self.showAll = true
						}
						uni.setStorageSync('user_token', res.token);
						uni.setStorageSync('user_no', res.info.user_no);
						uni.setStorageSync('user_info', res.info);
						var time = parseInt(new Date().getTime()) + 3500000;
						uni.setStorageSync('token_expire_time', time);
					}
					console.log('res', res)
					self.$Utils.finishFunc('tokenGet');
				};
				self.$apis.tokenGet(postData, callback);
			},

			showToast() {
				const self = this;
				uni.showModal({
					title: '',
					content: '功能开发中~',
					showCancel: false
				})
			},

			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
						if (self.userData.parent_no == '') {
							/* self.Router.redirectTo({
								route: {
									path: '/pages/invitation-code/invitation-code'
								}
							}) */
							self.showAll = true
						} else {
							self.showAll = true
						}
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},

			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2
				};
				postData.order = {
					listorder: 'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},

		}
	}
</script>

<style>
	.courseBox {
		padding-bottom: 170rpx;
	}

	.course-item {
		overflow: hidden;
	}

	.course-item image {
		width: 100%;
		height: 300rpx;
	}
	.course-item .wh20{width: 20rpx;height: 20rpx;margin-left: 5rpx;}
	.sign{width: auto;padding: 0 5rpx;}
</style>
