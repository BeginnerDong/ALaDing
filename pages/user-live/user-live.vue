<template>
	<view>
		
		<view class="p-3 pb-2 color2 line-h">
			<view class="font-40 font-w pb-4">2020年</view>
			<view class="font-26 fontw-600"><text class="font-42 font-w">08</text>2月</view>
		</view>
		<view class="text-center pb-4">
			<view class="color6 f5bj d-flex proHead">
				<view class="bb">商品名称</view>
				<view class="bb">商品ID</view>
			</view>
			<view class="d-flex pro" v-for="v in 4">
				<view class="bb">
					<view class="avoidOverflow2">鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋</view>
				</view>
				<view class="bb d-flex a-center j-center">
					<view class="avoidOverflow2">23569859454658754587</view>
				</view>
			</view>
		</view>
		
		<view class="p-3 pb-2 color2 line-h">
			<!-- <view class="font-40 pb-4 font-w">2020年</view> -->
			<view class="font-26 fontw-600"><text class="font-42 font-w">10</text>2月</view>
		</view>
		<view class="text-center pb-4">
			<view class="color6 f5bj d-flex proHead">
				<view class="bb">商品名称</view>
				<view class="bb">商品ID</view>
			</view>
			<view class="d-flex pro">
				<view class="bb">
					<view class="avoidOverflow2">鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋休闲男鞋</view>
				</view>
				<view class="bb d-flex a-center j-center">
					<view class="avoidOverflow2">23569859454658754587</view>
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
.fontw-600{font-weight: 600;}
</style>
