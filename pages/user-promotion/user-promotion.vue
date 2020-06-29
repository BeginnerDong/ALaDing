<template>
	<view>
		<view class="bgImg">
			<image src="../../static/images/to-promotel-img.png" mode=""></image>
		</view>
		
		<view class="position-relative bg-white mx-3 shadow text-center promoBox">
			<view class="bg fx rounded10 colorf">分享邀请有礼</view>
			<image src="../../static/images/coursel-img4.png" mode=""></image>
			<view class="font-36 color3 pt-4 pb-5">推广码：BGH5695S</view>
			<view class="btn bg">分享</view>
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
