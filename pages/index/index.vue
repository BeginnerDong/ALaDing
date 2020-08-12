<template>
	<view>
		
		<view class="position-relative pb-3">
			<image src="../../static/images/home-img.png" mode="widthFix" class="position-absolute top-0"></image>
			
			<view class="pt-2 px-3 position-relative">
				<view class="d-flex a-center px-3 ss">
					<image src="../../static/images/the host-icon.png" class="ss-icon mr-2"></image>
					<input type="text" value="" placeholder="搜索你想要推广的商品"/>
				</view>
				
				<view class="my-2 pb-2 d-flex a-center j-sb line-h colorf list">
					<view class="on">推荐</view>
					<view>服饰</view>
					<view>美妆护肤</view>
					<view>食品生鲜</view>
					<view>家居厨具</view>
					<view>数码产品</view>
				</view>
				
				<!-- banner -->
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#FF7B8E">
					<block>
						<swiper-item>
								<image src="../../static/images/the%20host-banner.png" ></image>
						</swiper-item>
					</block>
				</swiper>
				
			</view>
		</view>
		<view class="f5Bj-H20"></view>
		
		
		<view class="font-30 pt-4 d-flex j-center a-center colorM font-w line-h">
			<image src="../../static/images/home-icon1.png" class="icon"></image>
			<view class="px-3">今日推荐</view>
			<image src="../../static/images/home-icon.png" class="icon"></image>
		</view>
		
		<view class="mx-3 py-4 d-flex bB-e1">
			<view class="position-relative">
				<image src="../../static/images/car-img.png" class="wh250 rounded10"></image>
				<view class="tgTag">推广赚25</view>
			</view>
			<view class="d-flex flex-column pl-2" style="height: 250rpx;">
				<view class="font-30 flex-1 mb-2 avoidOverflow2">标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题标题</view>
				<view class="line-h color6 font-24">2563条评论 推广率76%</view>
				<view class="line-h py-3 color6">
					<text class="colorR pr-2">券后价￥99.0</text>
					<text class="font-24">京东价￥190.0</text>
				</view>
				<view class="line-h d-flex a-center font-26 colorf" style="line-height: 44rpx;">
					<view class="position-relative mr-2 text-center" style="height: 44rpx;width: 120rpx;">
						<image src="../../static/images/car-icon3.png" mode="widthFix"></image>
						<view class="position-absoluteXY pr-1">100元券</view>
					</view>
					<view class="Mbg d-flex a-center rounded px-1">
						<image src="../../static/images/car-icon.png" class="wh20"></image>
						<view>直播推广</view>
					</view>
				</view>
			</view>
		</view>
		
		
		
		<view style="height: 130rpx;"></view>
		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/course/course'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
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
				is_show: false
			}
		},
		onLoad() {
			const self = this;
			
		},
		methods: {
			
		}
	};
</script>
<style scoped>
.ss-icon{width: 29rpx;height: 29rpx;}
.ss{height: 60rpx;border-radius: 30rpx;background-color: #fff;}
input{flex: 1;background-color: #fff;font-size: 24rpx;}
.list{overflow-x: auto;}
.list view{margin-right: 30rpx;flex-shrink: 0;}
.list view:last-child{margin-right: 0;}
.list .on{position: relative;font-weight: bold;}
.list .on::before{content: '';background-color: #fff;width: 36rpx;height: 6rpx;border-radius: 5rpx;position: absolute;bottom: -15rpx;left: 50%;margin-left: -18rpx;}
swiper,swiper-item,swiper image{height: 300rpx;}

.icon{width: 174rpx;height: 13rpx;}
.colorR{color: #E81B1B;}
.tgTag{line-height: 44rpx;padding: 0 15rpx;background-color: rgba(0,0,0,0.4);color: #FFF;position: absolute;top: 0;left: 0;border-radius: 10rpx 0 10rpx 0;}
</style>
