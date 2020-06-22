<template>
	<view class="line-h">
		<view class="bg"></view>
		
		<view class="mx-3 bg-white rounded10 position-relative mt-5 shadow py-5 d-flex">
			<view class="text-center w-50 zb position-relative" @click="Router.navigateTo({route:{path:'/pages/user-teamList/user-teamList'}})">
				<view class="font-40 color2 pb-3 font-w">188</view>
				<view class="font-24 color2">我的主播 ></view>
			</view>
			<view class="text-center w-50" @click="Router.navigateTo({route:{path:'/pages/user-teamList/user-teamList'}})">
				<view class="font-40 color2 pb-3 font-w">10</view>
				<view class="font-24 color2">我的导师 ></view>
			</view>
		</view>
		
		<view class="teamBox1 px-3 bg-white">
			<view class="font-28 color2 pt-4">我的上级</view>
			<view class="item d-flex a-center py-3">
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
		
		<view class="teamBox2 px-3 bg-white mt-2">
			<view class="font-28 color2 pt-4">今日数据</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign3">主播</view>
					</view>
					<view class="color6">注册时间：2020.06.23 21:24:23</view>
				</view>
				<view class="font-40 qj" @click="Router.navigateTo({route:{path:'/pages/user-dataDetails/user-dataDetails'}})">></view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
					</view>
					<view class="color6">注册时间：2020.06.23 21:24:23</view>
				</view>
				<view class="qj font-40" @click="Router.navigateTo({route:{path:'/pages/user-dataDetails/user-dataDetails'}})">></view>
			</view>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign3">主播</view>
					</view>
					<view class="color6">注册时间：2020.06.23 21:24:23</view>
				</view>
				<view class="qj font-40" @click="Router.navigateTo({route:{path:'/pages/user-dataDetails/user-dataDetails'}})">></view>
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
	
.bg{height: 160rpx;background-color: #FF7B8E;position: fixed;top: 0;width: 100%;}

.zb::before{content: '';height: 50rpx;border-left: 1px dashed #d5d5d5;position: absolute;right: 0;top: 50%;margin-top: -25rpx;}

.teamBox1{padding-top: 74rpx;margin-top: -74rpx;}
.teamBox1 .item image{width: 100rpx;height: 100rpx;}
.teamBox2 .item image{width: 100rpx;height: 100rpx;}

.qj{color: #D5D5D5;width: 100rpx;text-align: right;height: 100rpx;line-height: 100rpx;}
</style>
