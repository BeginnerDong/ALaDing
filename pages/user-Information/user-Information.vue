<template>
	<view class="bg-white px-3 font-28">
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">头像</view>
			<image :src="userData.headImgUrl!=''?userData.headImgUrl:''" style="border-radius: 0;overflow: hidden;" class="userImg rounded-5"></image>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">昵称</view>
			<view class="color2">{{userData.nickname?userData.nickname:''}}</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb" v-if="userData.behavior>0">
			<view class="color6">邀请码</view>
			<view class="color2">{{userData.user_no?userData.user_no:''}}</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">微信号</view>
			<input type="text" v-model="wechat" placeholder="请输入" class="text-right font-22 color9"/>
		</view>
		<view class="py-4 borderB-f5">
			<view class="submit" @click="userInfoUpdate">确定</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userData:{},
				wechat:''
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getUserData'], self);
		},
		
		methods: {
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						self.wechat = self.userData.info.wechat
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			userInfoUpdate(){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					wechat:self.wechat
				};
				const callback = (res) => {
					if (res.solely_code==100000) {
						uni.navigateBack({
							delta:1
						})
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
.userImg{width: 80rpx;height: 80rpx;}
</style>
