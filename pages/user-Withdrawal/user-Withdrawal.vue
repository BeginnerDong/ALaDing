<template>
	<view>
		<view class="box bg-white mx-3 shadow">
			<view class="line-h py-5 px-3 d-flex a-center j-sb head">
				<view class="font-30 color2">到账银行卡</view>
				<view class="font-24 color2 d-flex"  @click="Router.navigateTo({route:{path:'/pages/user-backCard/user-backCard'}})">中国银行（2358）<view class="color9">></view></view>
			</view>
			<view class="py-5 font-24 color2 px-3">提现金额</view>
			<view class="picBox mx-3 borderB-f5 d-flex">
				<view>￥</view>
				<input type="text" value=""/>
			</view>
			<view class="font-24 color6 pt-3 pb-5 d-flex j-sb px-3">
				<view>本次可提现￥200.00</view>
				<view style="color: #fed513;">全部提现</view>
			</view>
			<view class="mt-5 submit mx-3">提现</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
.box{height: 632rpx;margin-top: 200rpx;}
.box .head{background-color: #fafafa;}

.picBox{font-size: 60rpx;color: #222;position: relative;}
.picBox input{height: 100%;}
</style>
