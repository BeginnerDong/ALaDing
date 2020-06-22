<template>
	<view>
		<view class="table">
			<view class="tr">
				<view class="th">日期</view>
				<view class="th">订单量</view>
				<view class="th">获得佣金</view>
				<view class="th">平台奖励</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
			</view>
			<view class="tr">
				<view class="td">2020.06.23</view>
				<view class="td">0</view>
				<view class="td">0</view>
				<view class="td">369</view>
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

<style>
page{background-color: #f5f5f5;}
.table{width: 100%;background-color: #fff;color: #222;}
.tr{display: flex;text-align: center;width: 100%;}
.th,.td{width: 25%;box-sizing: border-box;border-right: 1px solid #E1E1E1;height: 88rpx;line-height: 88rpx;}
.th:nth-child(4),.td:nth-child(4){border-right: none;}
.th{background-color: #fff2f4;font-size: 28rpx;}
.td{border-bottom: 1px solid #E1E1E1;font-size: 26rpx;}
</style>
