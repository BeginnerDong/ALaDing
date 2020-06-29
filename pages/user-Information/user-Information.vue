<template>
	<view class="bg-white px-3 font-28">
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">头像</view>
			<image src="../../static/images/about-img.png" class="userImg"></image>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">昵称</view>
			<view class="color2">碰火娃</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">邀请码</view>
			<view class="color2">154548JIui8</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">微信号</view>
			<input type="text" placeholder="请输入" class="text-right font-22 color9"/>
		</view>
		<view class="py-4 borderB-f5">
			<view class="submit">确定</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
.userImg{width: 80rpx;height: 80rpx;}
</style>
