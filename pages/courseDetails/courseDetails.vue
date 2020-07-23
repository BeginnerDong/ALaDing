<template>
	<view>
		<view class="banner">
			<swiper class="swiper-box"  indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-color="#d2d2d2" indicator-active-color="#dec193">
				<block v-for="(item,index) of mainData.bannerImg" :key="index">
					<swiper-item class="swiper-item">
						<image :src="item.url"  class="slide-image"></image>
					</swiper-item>
				</block>
				
			</swiper>
		</view>
		
		<view class="px-2 line-h rounded30-T bg-white position-relative title">
			<view class="pt-4 font-30 color2">{{mainData.title?mainData.title:''}}</view>
			<view class="py-2 font-26 color6 avoidOverflow2" style="line-height: 1.5;">{{mainData.description?mainData.description:''}}</view>
			<view class="d-flex a-center pb-3">
				<view class="price font-34 pr-1">{{mainData.price?mainData.price:''}}</view>
				<view class="sign">{{mainData.behavior==1?'主播':'导师'}}</view>
			</view>
		</view>
		<view class="px-3 bg-white mt-2"  :style="isIphoneX?'padding-bottom: 180rpx':''">
			<view class="content ql-editor" style="padding:0;"
			v-html="mainData.content">
			</view>
			
			<view class="position-fixed bottom-0 borderT-f5 left-0 right-0 bg-white px-3" :style="isIphoneX?'padding-bottom: 40rpx':''">
				<view class="submit my-2" @click="Router.navigateTo({route:{path:'/pages/courseBuy/courseBuy?id='+mainData.id}})">立即购买</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:{},
				isIphoneX:false
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.isIphoneX = wx.getStorageSync('isIphoneX');
			self.$Utils.loadAll(['getMainData'], self);
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
