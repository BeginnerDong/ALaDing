<template>
	<view>
		
		<view class="position-relative px-3 py-2">
			<view class="Mbg zbBg position-absoluteXY"></view>
			
			<view class="p-3 position-relative bg-white rounded10 shadowM">
				<view class="flex1">
					<image src="../../static/images/the host-img.png" class="anchorImg"></image>
					<view class="font-24 color6 pl-2 flex-1 flex5 anchorCon">
						<view class="flex">
							<view class="font-30 color2 font-w">小海南</view>
							<view class="tag tagP">全网</view>
						</view>
						<view>粉丝数量：2563.1万</view>
						<view>擅长品类：美妆护肤+美体+精油</view>
						<view>近3月直播：72场</view>
						<view>所属机构：小狗</view>
					</view>
				</view>
				
				<view class="flex0 colorM rounded10 borderM lxBtn">
					<image src="../../static/images/the host-icon5.png" class="wh32 mr-1"></image>
					<view>联系主播</view>
				</view>
			</view>
		</view>
		
		<view class="font-34 font-w mx-3 mt-3 anchorTit">主播档案</view>
		
		<view>
			<view class="flex0 py-3" >
				<image src="../../static/images/the host-icon6.png" class="anchorIcon"></image>
				<view class="font-32 font-w">PV</view>
			</view>
			<view class="qiun-charts">
				<!--#ifdef MP-ALIPAY -->
				<canvas canvas-id="canvasColumn" id="canvasColumn"></canvas>
				<!--#endif-->
				<!--#ifndef MP-ALIPAY -->
				<canvas canvas-id="canvasColumn" id="canvasColumn" class="charts"></canvas>
				<!--#endif-->
			</view>
			<view class="f5Bj-H20"></view>
		</view>
		
		<view>
			<view class="flex0 py-3" >
				<image src="../../static/images/the host-icon6.png" class="anchorIcon"></image>
				<view class="font-32 font-w">UV</view>
			</view>
			<view class="qiun-charts">
				<!--#ifdef MP-ALIPAY -->
				<canvas canvas-id="canvasColumn1" id="canvasColumn1" ></canvas>
				<!--#endif-->
				<!--#ifndef MP-ALIPAY -->
				<canvas canvas-id="canvasColumn1" id="canvasColumn1" class="charts"></canvas>
				<!--#endif-->
			</view>
			<view class="f5Bj-H20"></view>
		</view>
		
		
		
		
	</view>
</template>

<script>
	import uCharts from '../../components/uCharts/u-charts.js';
	var _self;
	var canvaColumn=null;
	export default {
		data() {
			return {
				
			}
		},
		onLoad(){
			canvaColumn=new uCharts({
				$this:_self,
					canvasId: 'canvasColumn',
					type: 'line',
					fontSize:11,
					colors:['#FF7B8E','#ba99ff'],
					legend:{show:true},
					dataLabel:true,
					dataPointShape:true,
					background:'#f5f5f5',
					pixelRatio:1,
					categories: ['3.10','3.15','3.20','3.25','3.31','4.05'],
					series: [{
						data:[102,65,301,122,465,32],
						'name':''
					}
					],
					animation: true,
					xAxis: {
						disableGrid:true,
						format:(val)=>{return val.toFixed(0)}
					},
					yAxis: {
						gridType:'solid',
						gridColor:'#f5f5f5',
						splitNumber:5,
						min:0,
						max:500,
						format:(val)=>{return val.toFixed(0)+'万'}
					},
					legend: {
						show: false
					},
					width: 400,
					height: 200,
					extra: {
						line:{
							type: 'canvas'
						}
					}
			});
		},
		methods: {
			
		}
	}
</script>

<style scoped>
.zbBg{height: 210rpx;}
.anchorImg{width: 180rpx;height: 220rpx;}
.anchorCon{height: 220rpx;}
.lxBtn{width: 400rpx;line-height: 70rpx;margin: 40rpx auto 10rpx;}
.anchorTit{position: relative;display: inline-block;z-index: 20;}
.anchorTit::before{position: absolute;content: '';width: 100%;height: 10rpx;bottom: 7rpx;background-color: #FF7B8E;z-index: -5;}

.anchorIcon{width: 50rpx;height: 22rpx;margin-right: 10rpx;}
.qiun-charts{width: 750rpx; height:380rpx;padding: 0 15rpx;}
.charts{width: 750rpx; height:380rpx;}

</style>