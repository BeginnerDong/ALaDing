<template>
	<view>
		
		<view class="p-3 d-flex a-center j-sb shadow">
			<view>全部商品({{mainData.length?mainData.length:'0'}})</view>
			<view @click="allDeltShow">{{!is_allDelt?'编辑':'完成'}}</view>
		</view>
		
		
		<view class="flex py-3 mx-3 j-ab bB-e1" v-for="(item,index) in mainData" :key="index">
			<image :src="item.isSelect?'../../static/images/car-icon1.png':'../../static/images/car-icon2.png'" @click="choose(index)" class="wh36 mr-2"></image>
			<view class="position-relative">
				<image :src="item.imageInfo.imageList[0].url" class="wh250 rounded10"></image>
				<view class="tgTag">推广赚{{item.commissionInfo.commission}}</view>
			</view>
			<view class="d-flex flex-column flex-1 pl-2" style="height: 250rpx;">
				<view class="font-30 flex-1 mb-2 avoidOverflow2">{{item.skuName}}</view>
				<view class="line-h color6 font-24">{{item.comments}}条评论 推广率{{item.goodCommentsShare}}%</view>
				<view class="line-h py-3 color6"  style="padding-top:25rpx">
					<text class="colorR pr-2">券后价￥{{item.priceInfo.lowestPrice}}</text>
					<text class="font-24">京东价￥{{item.priceInfo.price}}</text>
				</view>
				<view class="line-h d-flex a-center font-26 colorf" style="line-height: 44rpx;">
					<!-- <view class="position-relative mr-2 text-center" style="height: 44rpx;width: 120rpx;">
						<image src="../../static/images/car-icon3.png" mode="widthFix"></image>
						<view class="position-absoluteXY pr-1">100元券</view>
					</view>
					<view class="Mbg d-flex a-center rounded px-1">
						<image src="../../static/images/car-icon.png" class="wh20"></image>
						<view>直播推广</view>
					</view> -->
					<view style="color:#E81B1B">佣金比例{{item.commissionInfo.commissionShare}}%</view>
				</view>
			</view>
		</view>
		
		
		<view class="d-flex a-center j-sb px-3 bg-white shadowM bot">
			<view class="d-flex a-center">
				<image :src="isChooseAll?'../../static/images/car-icon1.png':'../../static/images/car-icon2.png'" class="wh36 mr-2"></image>
				<view @click="chooseAll">全选</view>
			</view>
			<view class="btn"  @click="pay" v-if="!is_allDelt">提交</view>
			<view class="btn delbtn" @click="deleteAll" v-if="is_allDelt">删除</view>
		</view>
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>产品</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/course/course'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>课程</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>主播</view>
			</view>
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/login/login'}})">
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
				status:true,
				mainData:[
					
				],
				is_allDelt:false,
				isChooseAll:true
			}
		},
		
		onShow() {
			const self = this;
			self.mainData = self.$Utils.getStorageArray('cartData');
			console.log('self.mainData',self.mainData)
			self.checkChooseAll();
		},
		
		methods: {
			
			
			
			pay(e) {
				const self = this;
				const dataArray = [];
				for (var i = 0; i < self.mainData.length; i++) {
					if (self.mainData[i].isSelect) {
						dataArray.push(
							{type:3,relation_user:self.mainData[i].skuId,thirdapp_id:2,passage_array:self.mainData[i],user_type:0,
							user_no:uni.getStorageSync('user_info').user_no},
						);
					};
				};
				if (dataArray.length == 0) {
					self.$Utils.showToast('未选择商品', 'none', 1000);
					return;
				};
				self.messageAdd(dataArray)
			},
			
			messageAdd(dataArray) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken'
				postData.dataArray = dataArray;
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('提交成功', 'none');
						var array = self.$Utils.getStorageArray('cartData');
						for (var i = 0; i < dataArray.length; i++) {
							for (var j = 0; j < array.length; j++) {
								if(dataArray[i].relation_user == array[j].skuId){
									self.$Utils.delStorageArray('cartData', array[j], 'skuId');
								}
							}
						};
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.messageAdd(postData, callback);
			},
			
			checkChooseAll() {
				const self = this;
				var isChooseAll = true;
				for (var i = 0; i < self.mainData.length; i++) {
					if (!self.mainData[i].isSelect) {
						isChooseAll = false;
					};
				};
				self.isChooseAll = isChooseAll;
			},
			
			chooseAll() {
				const self = this;
				self.isChooseAll = !self.isChooseAll;
				for (var i = 0; i < self.mainData.length; i++) {
					self.mainData[i].isSelect = self.isChooseAll;
					self.$Utils.setStorageArray('cartData', self.mainData[i], 'id', 999);
				};
				self.countTotalPrice();
			},
			
			allDeltShow(){
				const self = this;
				self.is_allDelt = !self.is_allDelt
			},
			
			counter(index,type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.$Utils.setStorageArray('cartData', self.mainData[index], 'id', 999);
				self.countTotalPrice();
			},
			
			deleteAll() {
				const self = this;
				uni.showModal({
					title: '提示',
					content: '确认要删除选中商品吗？',
					showCancel: true,
					cancelText: '取消',
					confirmText: '确认',
					success: res => {
						if (res.confirm) {
							for (var i = 0; i < self.mainData.length; i++) {
								if(self.mainData[i].isSelect){
									self.$Utils.delStorageArray('cartData', self.mainData[i], 'id');
								}
							};
							self.mainData = self.$Utils.getStorageArray('cartData');
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					},
				});
			},
			
			
			
			choose(index) {
				const self = this;
				
				if (self.mainData[index].isSelect) {
					self.mainData[index].isSelect = false;
				} else {
					self.mainData[index].isSelect = true;
				};
				self.$Utils.setStorageArray('cartData', self.mainData[index], 'id', 999);
				
				self.checkChooseAll();
				self.countTotalPrice();
			},
			
		}
	}
</script>

<style scoped >
.icon{width: 174rpx;height: 13rpx;}
.colorR{color: #E81B1B;}
.tgTag{line-height: 44rpx;padding: 0 15rpx;background-color: rgba(0,0,0,0.4);color: #FFF;position: absolute;top: 0;left: 0;border-radius: 10rpx 0 10rpx 0;}

.bot{height: 100rpx;position: fixed;bottom: 130rpx;left: 0;right: 0;}
.btn{height: 60rpx;border-radius: 30rpx;line-height: 60rpx;width: 160rpx;}
.delbtn{background-color: #fff;border: 1px solid #FF7B8E;color: #FF7B8E;}
</style>
