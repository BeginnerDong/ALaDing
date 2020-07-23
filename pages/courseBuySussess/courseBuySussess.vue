<template>
	<view>
		<view class="item  mx-3 px-3 py-3 bg-white rounded10 mt-3">
			<view class="font-24 color6 pb-3">订单号：268988745265658</view>
			<view class="d-flex">
				<image src="../../static/images/coursel-img1.png" mode=""></image>
				<view class="d-flex flex-column j-sb px-2 flex-1">
					<view class="font-28 color2 font-w">课程标题标题标题课程标题标题标题课程标题标题标题</view>
					<view class="d-flex a-center line-h ">
						<view class="price font-34 pr-2">1999</view>
						<view class="sign">主播</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="bg-white rounded10 m-3 p-3 color2 font-28">课程链接：http://www.iconfont.cn/search/index-indexhs</view>
		
		<view class="hx bg-white rounded10 d-flex flex-column a-center py-4 mx-3">
			<view class="font-28 color2 pb-4">课程核销码：GTDR58466</view>
			<image src="../../static/images/coursel-img4.png" mode=""></image>
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
.lj{width: 320rpx;}
.hx image{width: 260rpx;height: 260rpx;}
</style>
