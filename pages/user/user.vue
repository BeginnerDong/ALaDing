<template>
	<view class="user">
		<view class="head line-h ">
			<view class="userCon px-3 py-3 d-flex a-center">
				<image src="../../static/images/about-img.png" mode=""></image>
				<view class="colorf ml-2">
					<view class="d-flex a-center pb-3">
						<view class="pr-1 font-30">喷火娃</view>
						<view class="sign1">主播</view>
					</view>
					<view class="d-flex a-center">
						<view class="pr-1 font-26">邀请码：EK256D</view>
						<view class="sign1">复制</view>
					</view>
				</view>
			</view>
			<view class="font-50 colorf font-w text-center pt-3 pb-2">956.56</view>
			<view class="font-22 text-center colorf pb-3">可提现金额(￥)</view>
			<view class="d-flex j-center pb-4">
				<view class="btn1" @click="Router.navigateTo({route:{path:'/pages/user-Withdrawal/user-Withdrawal'}})">申请提现</view>
				<view class="btn1" @click="Router.navigateTo({route:{path:'/pages/user-WithdrawalRecord/user-WithdrawalRecord'}})">提现记录</view>
			</view>
		</view>
		
		<view class="userBox1 line-h text-center bg-white rounded10 d-flex mx-3">
			<view class="px-3 d-flex flex-column a-center j-center userBox1L">
				<view class="font-22 color2" style="padding-bottom: 25rpx;">本月平台奖励</view>
				<view class="font-30 color2">459.00</view>
			</view>
			<view class="flex-1">
				<view class="font-24 color2 py-3">推广佣金</view>
				<view class="d-flex">
					<view class="item">
						<view class="font-22 color9">本月预估结算金额</view>
						<view class="font-30 color2 py-2">356.00</view>
						<view class="font-22 color2 pb-3">已结算账单金额</view>
					</view>
					<view class="item">
						<view class="font-22 color9">下月预估结算金额</view>
						<view class="font-30 color2 py-2">356.00</view>
						<view class="font-22 color2 pb-3 djs">待结算</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="userBox2 bg-white mx-3 mt-2 rounded10">
			<view class="font-28 font-w mx-3 py-3 borderB-f5">常用工具</view>
			<view class="itemBox d-flex flex-wrap pb-4">
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-team/user-team'}})">
					<image src="../../static/images/about-icon.png" mode=""></image>
					<view>我的团队</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-promotion/user-promotion'}})">
					<image src="../../static/images/about-icon1.png" mode=""></image>
					<view>推广中心</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-profit/user-profit'}})">
					<image src="../../static/images/about-icon2.png" mode=""></image>
					<view>我的收益</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/user-aboutUs/user-aboutUs'}})">
					<image src="../../static/images/about-icon3.png" mode=""></image>
					<view>关于我们</view>
				</view>
				<view class="item" @click="Router.navigateTo({route:{path:'/pages/course/course'}})">
					<image src="../../static/images/about-icon4.png" mode=""></image>
					<view>专属客服</view>
				</view>
			</view>
		</view>
		
		<view class="footer">
			<view class="item">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/course/course'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item .on" @click="Router.navigateTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar5-a.png" mode=""></image>
				<view>我的</view>
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
	page{background-color: #F5F5F5;}
.head{background-color: #FF7B8E;padding-bottom: 100rpx;}
.userCon image{height: 120rpx;width: 120rpx;}

.userBox1{margin-top: -100rpx;}
.userBox1L{border-right: 1px dashed #d5d5d5;}
.userBox1 .item{width: 50%;}
.djs{color: #F51E1E;}


.itemBox .item{display: flex;align-items: center;width: 25%;flex-direction: column;font-size: 22rpx;color: #222;}
.itemBox .item image{width: 52rpx;height: 46rpx;margin: 40rpx 0 20rpx;}
</style>
