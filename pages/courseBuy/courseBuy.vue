<template>
	<view>
		<view class="item d-flex mx-3 px-3 py-3 bg-white rounded10 mt-3">
			<image src="../../static/images/coursel-img1.png" mode=""></image>
			<view class="d-flex flex-column j-sb px-2 flex-1">
				<view class="font-28 color2 font-w">课程标题标题标题课程标题标题标题课程标题标题标题</view>
				<view class="d-flex a-center line-h ">
					<view class="price font-34 pr-2">1999</view>
					<view class="sign">主播</view>
				</view>
			</view>
		</view>
		
		<view class="d-flex j-sb bg-white position-fixed bottom-0 left-0 right-0 courseFoot">
			<view class="px-3 d-flex a-center">
				合计<view class="price font-34 pr-2 pl-2">1999</view>
			</view>
			<view class="submitBtn colorf font-30 text-center" @click="Router.navigateTo({route:{path:'/pages/courseBuySussess/courseBuySussess'}})">确认订单</view>
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
.item image{width: 180rpx;height: 180rpx;border-radius: 10rpx;}
.courseFoot{height: 100rpx;}
.submitBtn{height: 100rpx;width: 280rpx;background-color: #FF7B8E;line-height: 100rpx;}
</style>
