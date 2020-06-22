<template>
	<view class="profit line-h">
		<view class="head">
			<view class="font-50 colorf font-w text-center pt-3 pb-2">956.56</view>
			<view class="font-22 text-center colorf pb-5">可提现金额(￥)</view>
		</view>
		<view class="proBox1 d-flex a-center j-sb rounded10 bg-white mx-3 shadow">
			<view class="item">
				<view class="font-30 color6 py-2">459.00</view>
				<view class="font-22 color6 pb-3">本月平台奖励</view>
			</view>
			<view class="item">
				<view class="font-30 color6 py-2">356.00</view>
				<view class="font-22 color6 pb-3">本月推广佣金</view>
			</view>
			<view class="item">
				<view class="btn2" @click="Router.navigateTo({route:{path:'/pages/user-Withdrawal/user-Withdrawal'}})">申请提现</view>
			</view>
		</view>
		
		<view class="d-flex j-sa borderB-f5 text-center proList">
			<view class="font-28 color2 proLi" :class="proLiCurrent==1?'on':''" @click="changeLi(1)">推广收益</view>
			<view class="font-28 color2 proLi" :class="proLiCurrent==2?'on':''" @click="changeLi(2)">全部收益</view>
			<view class="font-28 color2 proLi" :class="proLiCurrent==3?'on':''" @click="changeLi(3)">平台奖励</view>
		</view>
		
		<view class="proBox2 px-3">
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
					</view>
					<view class="color6">佣金比例：20%</view>
				</view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign3">导师</view>
					</view>
					<view class="color6">佣金比例：20%</view>
				</view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
					</view>
					<view class="color6">佣金比例：20%</view>
				</view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
					</view>
					<view class="color6">佣金比例：20%</view>
				</view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
					</view>
					<view class="color6">佣金比例：20%</view>
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
				proLiCurrent:1
			}
		},
		methods: {
			changeLi(i){
				const self = this;
				self.proLiCurrent = i;
			}
		}
	}
</script>

<style>
.profit .head{background-color: #FF7B8E;padding-bottom: 70rpx;}

.proBox1{margin-top: -70rpx;}
.proBox1 .item{width: 33.33%;text-align: center;position: relative;}
.proBox1 .item::before{content: '';height: 50rpx;border-left: 1px dashed #d5d5d5;position: absolute;right: 0;top: 50%;margin-top: -25rpx;}
.proBox1 .item:nth-child(3)::before{border-left: none;}
.btn2{margin: 0 35rpx;}

.proLi{padding: 40rpx 0 30rpx;width: 33.33%;}
.proList .on{color: #FF7B8E;font-weight: 700;position: relative;}
.proList .on::before{content:'';width: 30rpx;height: 4rpx;background-color: #FF7B8E;position: absolute;bottom: 0;left: 50%;margin-left: -15rpx;}

.proBox2 image{width: 100rpx;height: 100rpx;}
</style>
