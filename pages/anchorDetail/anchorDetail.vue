<template>
	<view>

		<view class="position-relative px-3 py-2">
			<view class="Mbg zbBg position-absoluteXY"></view>

			<view class="p-3 position-relative bg-white rounded10 shadowM">
				<view class="flex1">
					<image :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" class="anchorImg"></image>
					<view class="font-24 color6 pl-2 flex-1 flex5 anchorCon">
						<view class="flex">
							<view class="font-30 color2 font-w">{{mainData.name?mainData.name:''}}</view>
							<view class="tag" v-for="(item,index) in mainData.anchorPlant" :key="index">{{item}}</view>
						</view>
						<view>粉丝数量：{{mainData.fansCount?mainData.fansCount:''}}万</view>
						<view>擅长品类：{{mainData.goodAt?mainData.goodAt:''}}</view>
						<view>近3月直播：{{anchorSession}}场</view>
						<view>所属机构：{{mainData.institute?mainData.institute:''}}</view>
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
			<view class="flex0 py-3">
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
			<view class="flex0 py-3">
				<image src="../../static/images/the host-icon6.png" class="anchorIcon"></image>
				<view class="font-32 font-w">UV</view>
			</view>
			<view class="qiun-charts">
				<!--#ifdef MP-ALIPAY -->
				<canvas canvas-id="canvasColumn1" id="canvasColumn1"></canvas>
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
	var canvaColumn = null;
	export default {
		data() {
			return {
				mainData: {},
				anchorSession:0
			}
		},
		onLoad(options) {
			const self = this;
			self.user_no = options.user_no;
			self.$Utils.loadAll(['getMainData', 'getLogData'], self);

		},
		methods: {

			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no: self.user_no,
					user_type: 0
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0]
						self.mainData.anchorPlant = self.mainData.anchorPlant.split(',')
						self.mainData.goodAt = self.mainData.goodAt.split(',')
						self.mainData.goodAt = self.mainData.goodAt.join('+')
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userInfoGet(postData, callback);
			},

			getLogData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.order = {
					anchorTime: 'asc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						var date = [];
						var pv = [];
						var uv = [];
						for (var i = 0; i < res.info.data.length; i++) {
							date.push(res.info.data[i].result.substr(5, 10));
							pv.push(res.info.data[i].pv)
							uv.push(res.info.data[i].pv)
							self.anchorSession += parseInt( res.info.data[i].anchorSession)
						};
						canvaColumn = new uCharts({
							$this: _self,
							canvasId: 'canvasColumn',
							type: 'line',
							enableScroll: true, //开启图表拖拽功能
							fontSize: 11,
							colors: ['#FF7B8E', '#ba99ff'],
							legend: {
								show: true
							},
							dataLabel: true,
							dataPointShape: true,
							background: '#f5f5f5',
							pixelRatio: 1,
							categories: date,
							series: [{
								data: pv,
							}],
							animation: true,
							xAxis: {
								disableGrid: true,
								//scrollShow:true,//新增是否显示滚动条，默认false
								//scrollAlign:'left',//滚动条初始位置
								itemCount: 6
							},
							yAxis: {
								gridType: 'solid',
								gridColor: '#f5f5f5',
								splitNumber: 5,
								min: 0,
								max: 500,
								format: (val) => {
									return val.toFixed(0)
								}
							},
							legend: {
								show: false
							},
							width: 400,
							height: 200,
							extra: {
								line: {
									type: 'canvas'
								}
							}
						});

					};
					self.$Utils.finishFunc('getLogData');
				};
				self.$apis.logGet(postData, callback);
			},

		}
	}
</script>

<style scoped>
	.zbBg {
		height: 210rpx;
	}

	.anchorImg {
		width: 180rpx;
		height: 220rpx;
	}

	.anchorCon {
		height: 220rpx;
	}

	.lxBtn {
		width: 400rpx;
		line-height: 70rpx;
		margin: 40rpx auto 10rpx;
	}

	.anchorTit {
		position: relative;
		display: inline-block;
		z-index: 20;
	}

	.anchorTit::before {
		position: absolute;
		content: '';
		width: 100%;
		height: 10rpx;
		bottom: 7rpx;
		background-color: #FF7B8E;
		z-index: -5;
	}

	.anchorIcon {
		width: 50rpx;
		height: 22rpx;
		margin-right: 10rpx;
	}

	.qiun-charts {
		width: 750rpx;
		height: 380rpx;
		padding: 0 15rpx;
	}

	.charts {
		width: 750rpx;
		height: 380rpx;
	}
</style>
