<template>
	<view>
		
		<view class="p-3 d-flex a-center j-sb shadow">
			<view>全部商品(2)</view>
			<view @click="changeStatus">{{status?'编辑':'完成'}}</view>
		</view>
		
		
		<view class="flex py-3 mx-3 j-ab bB-e1" v-for="v in 2">
			<image src="../../static/images/car-icon2.png" class="wh36 mr-2"></image>
			<view class="position-relative">
				<image src="../../static/images/car-img.png" class="wh250 rounded10"></image>
				<view class="tgTag">推广赚25</view>
			</view>
			<view class="d-flex flex-column flex-1 pl-2" style="height: 250rpx;">
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
		
		
		<view class="d-flex a-center j-sb px-3 bg-white shadowM bot">
			<view class="d-flex a-center">
				<image src="../../static/images/car-icon2.png" class="wh36 mr-2"></image>
				<view>全选</view>
			</view>
			<view class="btn" :class="status?'':'delbtn'">{{status?'去支付':'删除'}}</view>
		</view>
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
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
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
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
				status:true
			}
		},
		methods: {
			
			changeStatus(){
				const self = this;
				self.status = !self.status;
			}
			
		}
	}
</script>

<style scoped >
.icon{width: 174rpx;height: 13rpx;}
.colorR{color: #E81B1B;}
.tgTag{line-height: 44rpx;padding: 0 15rpx;background-color: rgba(0,0,0,0.4);color: #FFF;position: absolute;top: 0;left: 0;border-radius: 10rpx 0 10rpx 0;}

.bot{height: 100rpx;position: fixed;bottom: 130rpx;left: 0;right: 0;}
.btn{height: 60rpx;border-radius: 30rpx;line-height: 60rpx;width: 160rpx;}
.delbtn{background-color: #fff;border: 1px solid #FF7B8E;color: #FF7B8E;}
</style>
