<template>
	<view>
		
		<view class="px-3 py-2 Mbg">
			 <view class="bg-white rounded30 flex1 px-3">
				 <image src="../../static/images/the host-icon.png" class="wh29 p-a mr-2"></image>
				 <input type="text" value="" placeholder="搜索你想要推广的商品" />
			 </view>
		</view>
		
		<!-- banner -->
		<view class="banner m-3">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#FF7B8E">
				<swiper-item>
					<image src="../../static/images/the host-banner.png" ></image>
				</swiper-item>
			</swiper>
		</view>
		
		<view class="font-30 font-w line-h px-3 pb-3 pt-2">优质主播推荐</view>
		<view class="font-24 line-h flex2 bB-f5 shadowB z-index10 nav">
			<view class="flex py-3" @click="Show(1)" :class="navCurr==1&&tj_show?'on':''">
				<view>擅长类型</view>
				<image src="../../static/images/the host-icon3.png" class="sj-icon" v-if="navCurr==1&&tj_show"></image>
				<image src="../../static/images/the host-icon1.png" class="sj-icon" v-else></image>
			</view>
			<view class="flex py-3" @click="Show(2)" :class="navCurr==2&&tj_show?'on':''">
				<view>粉丝数</view>
				<image src="../../static/images/the host-icon3.png" class="sj-icon" v-if="navCurr==2&&tj_show"></image>
				<image src="../../static/images/the host-icon1.png" class="sj-icon" v-else></image>
			</view>
			<view class="flex py-3" @click="Show(3)" :class="navCurr==3&&tj_show?'on':''">
				<view>客单价</view>
				<image src="../../static/images/the host-icon3.png" class="sj-icon" v-if="navCurr==3&&tj_show"></image>
				<image src="../../static/images/the host-icon1.png" class="sj-icon" v-else></image>
			</view>
		</view>
		
		<view class="px-3 py-1 position-relative">
			<!-- 导航弹框 -->
			<view class="anchor-mask" v-show="tj_show">
				<view class="px-3 bg-white rounded20-B">
					<view class="flex1 font-26 py-4 bB-e1" v-for="(v,i) in 3" :key="i" @click="changeLi(i)">
						<view>不限</view>
						<image src="../../static/images/the host-icon4.png" class="yes-icon" v-show="liCurr==i"></image>
					</view>
				</view>
			</view>
			
			<!-- 主播列表 -->
			<view class="flex1 py-3 bB-e1 anchor" v-for="v in 5" @click="Router.navigateTo({route:{path:'/pages/anchorDetail/anchorDetail'}})" :key="i">
				<image src="../../static/images/the host-img.png" class="anchorImg"></image>
				<view class="font-24 color6 pl-2 flex-1 flex5 py-1 anchorCon">
					<view class="flex">
						<view class="font-30 color2 font-w">小海南</view>
						<view class="tag tagP">全网</view>
						<view class="tag tagR">京东</view>
						<view class="tag tagB">抖音</view>
					</view>
					<view>粉丝数量：2563.1万</view>
					<view>客单价：95.56元</view>
					<view>近3月直播：72场</view>
				</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon"></image>
			</view>
		</view>
		
		
		
		
		<view style="height: 130rpx;"></view>
		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item"   @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/course/course'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item"   @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
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
				Router:this.$Router,
				tj_show:false,
				navCurr:0,
				liCurr:0
			}
		},
		methods: {
			Show(i){
				const self = this;
				if(self.navCurr != i){
					self.tj_show = true;
					self.navCurr = i
				}else{
					self.tj_show = false;
					self.navCurr = 0
				}
				
			},
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
		}
	}
</script>

<style scoped>
input{font-size: 24rpx;height: 60rpx;flex: 1;}
.banner swiper{width: 690rpx;height: 300rpx;}
.banner image{border-radius: 10rpx;}
.anchorImg{width: 150rpx;height: 180rpx;}
.anchorCon{height: 180rpx;}
.anchor:nth-child(1){border: none!important;}

.nav .on{color: #FF7B8E;}
.anchor-mask{height: 100%;position: absolute;top: 0;left: 0;bottom: 0;right: 0;background-color: rgba(0,0,0,0.4);z-index: 2;}
</style>
