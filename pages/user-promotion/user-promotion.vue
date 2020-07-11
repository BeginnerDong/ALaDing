<template>
	<view>
		<view class="bgImg">
			<image src="../../static/images/to-promotel-img.png" mode=""></image>
		</view>
		
		<view class="position-relative bg-white mx-3 shadow text-center promoBox">
			<view class="bg fx rounded10 colorf">分享邀请有礼</view>
			<image :src="QrData.url?QrData.url:''" mode=""></image>
			<view class="font-36 color3 pt-4 pb-5">推广码：{{userData.user_no?userData.user_no:''}}</view>
			<view class="btn bg"  @click="save">保存到相册</view>
		</view>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				userData:{},
				QrData:{}
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getUserData','getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken'
				postData.qrInfo = {
					scene: wx.getStorageSync('user_info').user_no,
					page: 'pages/invitation-code/invitation-code',
				};
				postData.output = 'url';
				postData.ext = 'png';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.QrData = res.info;
					} else {
						self.$Utils.showToast(res.msg, 'none')
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.getQrCode(postData, callback);
			},
			
			save() {
				let self = this
				//若二维码未加载完毕，加个动画提高用户体验
				wx.showToast({
					icon: 'loading',
					title: '正在下载图片',
					duration: 1000
				})
				//判断用户是否授权"保存到相册"
				wx.getSetting({
					success(res) {
						//没有权限，发起授权
						if (!res.authSetting['scope.writePhotosAlbum']) {
							wx.authorize({
								scope: 'scope.writePhotosAlbum',
								success() { //用户允许授权，保存图片到相册
									self.savePhoto();
								},
								fail() { //用户点击拒绝授权，跳转到设置页，引导用户授权
								console.log('fail')
									wx.showToast({
										icon: 'none',
										title: '请至小程序设置中开启相册权限',
										duration: 1000
									})
								}
							})
						} else { //用户已授权，保存到相册
							self.savePhoto()
						}
					}
				})
			},
			//保存图片到相册，提示保存成功
			savePhoto() {
				let self = this
				wx.downloadFile({
					url: self.QrData.url,
					success: function(res) {
						wx.saveImageToPhotosAlbum({
							filePath: res.tempFilePath,
							success(res) {
								wx.showToast({
									title: '保存成功',
									icon: "success",
									duration: 1000
								})
							}
						})
					}
				})
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
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
page{background-color: #ffeff1;}

.bgImg{position: fixed;top: 0;height: 1023rpx;width: 100%;}
.bgImg image{height: 100%;width: 100%;}
.bgImg::before{content: '';width: 100%;height: 50rpx;background-color: #FF7B8E;position: absolute;top: 0;}

.promoBox{height: 600rpx;border-radius: 50rpx;top: 550rpx;}
.promoBox image{width: 240rpx;height: 240rpx;margin: 10rpx auto 0;}

.bg{background: linear-gradient(to right, #FF7B8E , #FF97A6);}
.fx{width: 420rpx;height: 80rpx;line-height: 80rpx;position: relative;top: -30rpx;margin: 0 auto;}
.btn{margin: 0 auto;}
</style>
