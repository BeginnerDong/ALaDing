<template>
	<view v-if="showAll">
		<view class="bgImg position-fixed top-0 left-0 right-0">
			<image src="../../static/images/the-invitationl-icon.png" mode=""></image>
		</view>
		<view class="invi-txt text-center position-relative top-0 w-100">
			<image src="../../static/images/the-invitationl-img.png" mode=""></image>
			<view class="font-30 colorf pt-5 pb-2">帮你实现不止“3”个愿望</view>
			<view class="font-24 colorf pb-2">社交+电商+短视频+直播带货</view>
			<view class="font-24 colorf pb-3">挑选属于你的优质主播  让直播带货更简单</view>
		</view>
		<view class="inviCard mx-3 rounded20 position-relative mt-2 shadow">
			<!-- 没有邀请码 -->
			<view class="d-flex flex-column a-center" v-if="codeCurrent==1">
				<view class="font-3 color2 font-w py-5 mt-2">请输入邀请码</view>
				<input type="text" style="padding: 0 20rpx;font-weight: 700;" v-model="code" @blur="searchUser()"/>
				<view class="font-24 pt-3 txt" @click="maskShow()">没有邀请码？</view>
			</view>
			
			<!-- 换个邀请码 -->
			<view class="d-flex flex-column a-center" v-else>
				<view class="font-3 color2 font-w py-5 mt-2">请确认您的邀请人</view>
				<view class="inviPer" style="text-align: center;">
					<image style="border-radius: 50%;overflow: hidden;" :src="shareUser.headImgUrl!=''?shareUser.headImgUrl:''" mode=""></image>
					<view class="font-32 color2 pt-3">{{shareUser.nickname}}</view>
				</view>
				<view class="font-24 pt-3 txt" @click="changeCode(1)">我想换个邀请码</view>
			</view>
			
			<view class="position-absolute bottom-0 d-flex flex-column a-center w-100">
				<button class="btn" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">下一步</button>
				<view class="tips d-flex j-center a-center pt-3">
					<image src="../../static/images/the-invitationl-icon1.png" mode=""></image>
					<view class="px-1 font-22">友情提示：请确认您的邀请人，注册后不可以更改哦</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				codeCurrent:1,
				code:'',
				shareUser:{},
				showAll:false
			}
		},
		
		onLoad(options) {
			const self = this;
			if(options.scene){
				var scene = decodeURIComponent(options.scene);
				self.code = scene;
				self.searchUser()
			};
			self.$Utils.loadAll(['getUserData'], self);
			
		},
		
		
		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				
				return {
					title:'阿拉丁',
					path: '/pages/index/index', //点击分享的图片进到哪一个页面
					//imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
					success: function(res) {
						// 转发成功
						
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			}else{
				return {
					title:'阿拉丁',
					path: '/pages/index/index', //点击分享的图片进到哪一个页面
					//imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
					success: function(res) {
						// 转发成功
						
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			}
		},
		
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.userData.parent_no!=''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('您的账号已被邀请', 'none');
					return
				};
				if(self.code == self.userData.user_no){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('不可自己邀请自己', 'none');
					return
				};
				if(JSON.stringify(self.shareUser)=="{}"){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('邀请人信息错误', 'none');
					return
				};			
				const callback = (user, res) => {
					console.log(res)
					self.userUpdate();
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			userUpdate(){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					parent_no:self.shareUser.user_no
				};
				if(!wx.getStorageSync('user_info')||wx.getStorageSync('user_info').headImgUrl==''||!wx.getStorageSync('user_info').headImgUrl){
				  postData.refreshToken = true;
				};
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.Router.redirectTo({route:{path:'/pages/user/user'}})
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userUpdate(postData, callback);
			},
			
			searchUser(){
				const self = this;
				const postData = {};
				console.log(222)
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:self.code
				};
				const callback = (res) => {
					if (res.solely_code==100000&&res.info.data.length > 0) {
						self.codeCurrent = 2;
						self.shareUser = res.info.data[0]
					}else{
						uni.showModal({
							title:'提示',
							content:'此邀请码未找到对应用户',
							showCancel:false,
							confirmText:'我知道了',
							success(res) {
								if(res.confirm){
									self.code=''
								}
							}
						})
					}
				};
				self.$apis.commonUserGet(postData, callback);
			},
			
			maskShow(){
				const self = this;
				uni.showModal({
					title:'提示',
					content:'请联系身边已注册阿拉丁的朋友索要或网络搜索阿拉丁邀请码',
					showCancel:false,
					confirmText:'知道了',
					success(res) {
						if(res.confirm){
						}
					}
				})
			},
			
			changeCode(i){
				const self = this;
				self.codeCurrent = i;
				self.code = '';
			},
			
			
			getUserData() {
				const self = this;
				const postData = {};
				console.log(222)
				postData.tokenFuncName = 'getProjectToken';
				
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						self.showAll = true
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
		}
	}
</script>

<style>
page{width: 100%;height: 100%;}
.bgImg image{height: 440rpx;}
.invi-txt image{width: 184rpx;height: 58rpx;margin: 0 auto;}
.inviCard{height: 784rpx;width: 690rpx;background-color: #fff;}
.inviCard input{height: 80rpx;width: 540rpx;border: 1px solid #d5d5d5;border-radius: 40rpx;}
.inviCard .txt{color: #fed513;}

.inviPer image{width: 100rpx;height: 100rpx;}


.tips{color: #ed1b1b;padding-bottom: 90rpx;}
.tips image{width: 24rpx;height: 24rpx;}

.maskBox{width: 600rpx;height: 300rpx;}
</style>
