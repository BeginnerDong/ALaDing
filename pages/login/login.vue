<template>
	<view>
		
		<view class="position-relative">
			<image src="../../static/images/thelogin-img1.png" class="loginBg"></image>
			<image src="../../static/images/thelogin-img.png" class="nameImg"></image>
		</view>
		
		<view class="mx65 d-flex a-start">
			<image src="../../static/images/thelogin-icon.png" class="dh-icon mr-3"></image>
			<input type="text" value="" placeholder="输入手机号码" />
		</view>
		<view class="mx65 d-flex a-start">
			<image src="../../static/images/thelogin-icon1.png" class="aq-icon mr-3"></image>
			<input type="text" value="" placeholder="输入验证码" />
		</view>
		
		<view class="btn600" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">确定</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.loginBg{height: 338rpx;}
.nameImg{width: 244rpx; height: 77rpx;position: absolute;top: 0;left: 0;right: 0;bottom: 0;margin: auto;}
.dh-icon{width: 29rpx;height: 43rpx;}
.aq-icon{width: 36rpx;height: 40rpx;margin-left: -4rpx;}
input{height: 64rpx;font-size: 24rpx;flex: 1;border-bottom: 1px solid #e1e1e1;}
.mx65{margin-left: 65rpx;margin-right: 65rpx;margin-top: 60rpx;}
.btn600{margin: 100rpx auto;}
</style>
