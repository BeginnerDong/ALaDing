<template>
	<view>
		<view class="mx-3 rounded10 shadow-sm mt-2 course-item" @click="Router.navigateTo({route:{path:'/pages/courseDetails/courseDetails'}})">
			<image src="../../static/images/coursel-img.png" mode=""></image>
			<view class="px-2 line-h">
				<view class="py-3 font-30 color2">课程标题标题标题</view>
				<view class="d-flex a-center pb-3">
					<view class="price font-34 pr-1">1999</view>
					<view class="sign">主播</view>
				</view>
			</view>
		</view>
		<view class="mx-3 rounded10 shadow-sm mt-2 course-item" @click="Router.navigateTo({route:{path:'/pages/courseDetails/courseDetails'}})">
			<image src="../../static/images/coursel-img1.png" mode=""></image>
			<view class="px-2 line-h">
				<view class="py-3 font-30 color2">课程标题标题标题</view>
				<view class="d-flex a-center pb-3">
					<view class="price font-34 pr-1">1999</view>
					<view class="sign">主播</view>
				</view>
			</view>
		</view>
		
		
		<view class="footer">
			<view class="item">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item .on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
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
			<view class="item" @click="Router.navigateTo({route:{path:'/pages/user/user'}})">
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
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.course-item{overflow: hidden;}
.course-item image{width: 100%;height: 300rpx;}

</style>
