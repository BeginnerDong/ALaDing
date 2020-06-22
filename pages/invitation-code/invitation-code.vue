<template>
	<view>
		<view class="bgImg position-fixed top-0 left-0 right-0">
			<image src="../../static/images/the%20invitationl-icon.png" mode=""></image>
		</view>
		<view class="invi-txt text-center position-relative top-0 w-100">
			<image src="../../static/images/the invitationl-img.png" mode=""></image>
			<view class="font-30 colorf pt-5 pb-3">实现你3个愿望~阿拉丁</view>
			<view class="font-24 colorf pb-3">京东海量专属优惠，购买省钱 | 分享赚钱</view>
		</view>
		<view class="inviCard mx-3 rounded20 position-relative mt-2 shadow">
			<!-- 没有邀请码 -->
			<view class="d-flex flex-column a-center" v-if="codeCurrent==1">
				<view class="font-3 color2 font-w py-5 mt-2">请输入邀请码</view>
				<input type="text" value=""  @click="changeCode(2)"/>
				<view class="font-24 pt-3 txt" @click="maskShow()">没有邀请码？</view>
			</view>
			
			<!-- 换个邀请码 -->
			<view class="d-flex flex-column a-center" v-else>
				<view class="font-3 color2 font-w py-5 mt-2">请确认您的邀请人</view>
				<view class="inviPer">
					<image src="../../static/images/the%20invitationl-img1.png" mode=""></image>
					<view class="font-32 color2 pt-3">Tahoe</view>
				</view>
				<view class="font-24 pt-3 txt" @click="changeCode(1)">我想换个邀请码</view>
			</view>
			
			<view class="position-absolute bottom-0 d-flex flex-column a-center w-100">
				<view class="btn" @click="Router.navigateTo({route:{path:'/pages/course/course'}})">下一步</view>
				<view class="tips d-flex j-center a-center pt-3">
					<image src="../../static/images/the%20invitationl-icon1.png" mode=""></image>
					<view class="px-1 font-22">友情提示：请确认您的邀请人，注册后不可以更改哦</view>
				</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="mask_show">
			<view class="maskBox bg-white rounded10 text-center position-absolute left-0 top-0 right-0 bottom-0 m-a">
				<view class="font-26 color2 font-w py-3">提示</view>
				<view class="font-24 color6 pb-4 px-4 mx-3 line-h-md">请联系身边已注册阿拉丁的朋友索要或网络搜索阿拉丁邀请码</view>
				<view class="font-28 font-w borderT-f5 py-3" @click="maskShow()">知道了</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mask_show:false,
				codeCurrent:1
			}
		},
		methods: {
			maskShow(){
				const self = this;
				self.mask_show = !self.mask_show;
			},
			changeCode(i){
				const self = this;
				self.codeCurrent = i;
			}
		}
	}
</script>

<style>
page{width: 100%;height: 100%;}
.bgImg image{height: 440rpx;}
.invi-txt image{width: 184rpx;height: 58rpx;margin: 0 auto;}
.inviCard{height: 784rpx;width: 690rpx;background-color: #fff;}
.inviCard input{height: 80rpx;width: 540rpx;border: 1px solid #d5d5d5;border-radius: 40rpx;}
.inviCard .txt{color: #fed513;}

.inviPer image{width: 100rpx;height: 100rpx;}


.tips{color: #ed1b1b;padding-bottom: 90rpx;}
.tips image{width: 24rpx;height: 24rpx;}

.maskBox{width: 600rpx;height: 300rpx;}
</style>
