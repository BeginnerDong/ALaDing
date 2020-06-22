<template>
	<view>
		<view class="banner">
			<swiper class="swiper-box"  indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-color="#d2d2d2" indicator-active-color="#dec193">
				<block>
					<swiper-item class="swiper-item">
						<image src="../../static/images/coursel-img1.png"  class="slide-image"></image>
					</swiper-item>
				</block>
				<block>
					<swiper-item class="swiper-item">
						<image src="../../static/images/coursel-img.png"  class="slide-image"></image>
					</swiper-item>
				</block>
			</swiper>
		</view>
		
		<view class="px-2 line-h rounded30-T bg-white position-relative title">
			<view class="py-4 font-30 color2">课程标题标题标题</view>
			<view class="d-flex a-center pb-3">
				<view class="price font-34 pr-1">1999</view>
				<view class="sign">主播</view>
			</view>
		</view>
		<view class="px-3 bg-white mt-2">
			<view class="font-30 color6 pt-4">课程简介</view>
			<view class="color2 font-28 pt-4">
				里手动出我把从部分是do财经网啤酒开辟可接受的花覅胡搜日奇偶给爱豆世纪欧非好吧解耦给安徽金凤凰稳如分红解耦给后访问里手动出我把从部分
			</view>
			<view class="color2 font-28 pt-4">
				里手动出我把从部分是do财经网啤酒开辟可接受的花覅胡搜日奇偶给爱豆世纪欧非好吧解耦给安徽金凤凰稳如分红解耦给后访问里手动出我把从部分
			</view>
			<view class="imgBox pt-3">
				<image src="../../static/images/coursel-img2.png" mode=""></image>
			</view>
			
			<view class="position-fixed bottom-0 borderT-f5 left-0 right-0 bg-white px-3">
				<view class="submit my-2" @click="Router.navigateTo({route:{path:'/pages/courseBuy/courseBuy'}})">立即购买</view>
			</view>
		</view>
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

<style>
page{background-color: #f5f5f5;}
.swiper-box{height: 440rpx;}
.slide-image{width: 100%;height: 440rpx;}
.title{margin-top: -40rpx;}
.imgBox{padding-bottom: 250rpx;}
.imgBox image{width: 100%;height: 900rpx;}
</style>
