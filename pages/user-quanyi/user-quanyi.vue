<template>
	<view>
		
		<view class="text-center position-relative">
			<image src="../../static/images/quanyi-img.png" class="qyBg"></image>
			
			<view class="position-absoluteXY line-h">
				<view class="txt1 c1 font-50 pb-2">身份权益</view>
				<view class="c1 font-26">购买身份会员享受带来的</view>
				<view class="txt2 font-36 font-w">购买课程享受权益</view>
				
				<view class="con text-left">
					<view class="d-flex a-center conTxt" v-for="(v,i) in 5">
						<view class="position-relative pr-2">
							<image src="../../static/images/quanyi-icon.png" class="wh70"></image>
							<view class="position-absoluteXY wh70 line70 font-50 text-center colorf">{{i+1}}</view>
						</view>
						<view>你度搜为和的农夫和我额符号你度搜为和的农夫和我额符号</view>
					</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.qyBg{height: 1335rpx;}
.c1{color: #CDBBA1;}
.txt1{margin-top: 227rpx;}
.txt2{color: #926C35;margin-top: 72rpx;}
.con{padding-top: 46rpx;}
.conTxt{margin: 68rpx 93rpx 0;}
.line70{line-height: 70rpx;}
</style>
