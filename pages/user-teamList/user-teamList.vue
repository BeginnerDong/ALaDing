<template>
	<view>
		<view class="color2 font-30 d-flex a-center text-center head shadow z-index10">
			<view class="w-50 title position-relative" :class="titCurrent==1?'on':''" @click="changeTit(1)">主播</view>
			<view class="w-50 title position-relative" :class="titCurrent==2?'on':''" @click="changeTit(2)">导师</view>
		</view>
		<!-- 主播列表 -->
		<view class="teamListBox px-3 bg-white mt-3" v-if="titCurrent == 1">
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
						<view class="sign3">主播</view>
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
		
		<!-- 导师列表 -->
		<view class="teamListBox px-3 bg-white mt-3" v-else>
			<view class="item d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/teaml-img.png" mode=""></image>
				<view class="font-26 pl-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">金刚葫芦娃 15235648571</view>
						<view class="sign2">导师</view>
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
						<view class="sign2">导师</view>
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
				Router:this.$Router,
				titCurrent:1
			}
		},
		methods: {
			changeTit(i){
				const self = this;
				self.titCurrent = i;
			}
		}
	}
</script>

<style>
.head{height: 90rpx;line-height: 90rpx;}
.head .on{color: #FF7B8E;font-weight: 700;}
.head .on::before{content:'';width: 30rpx;height: 4rpx;background-color: #FF7B8E;position: absolute;bottom: 0;left: 50%;margin-left: -15rpx;}

.teamListBox .item image{width: 100rpx;height: 100rpx;}
.qj{color: #D5D5D5;width: 100rpx;text-align: right;height: 100rpx;line-height: 100rpx;}
</style>
