<template>
	<view v-if="showAll">
		
		<view class="position-relative pb-3">
			<image src="../../static/images/home-img.png" mode="widthFix" class="position-absolute top-0"></image>
			
			<view class="pt-2 px-3 position-relative">
				<view class="d-flex a-center px-3 ss">
					<image src="../../static/images/the host-icon.png" class="ss-icon mr-2"></image>
					<input type="text" value="" placeholder="京东接口暂未支持"/>
				</view>
				
				<view class="my-2 pb-2 d-flex a-center j-sb line-h colorf list">
					<view :class="post.eliteId==23?'on':''" @click="change(23)">为你推荐</view>
					<view :class="post.eliteId==22?'on':''" @click="change(22)">实时热销榜</view>
					<view :class="post.eliteId==1?'on':''" @click="change(1)">好券商品</view>
					<view :class="post.eliteId==2?'on':''" @click="change(2)">精选卖场</view>
					<view :class="post.eliteId==10?'on':''" @click="change(10)">9.9包邮</view>
					<view :class="post.eliteId==15?'on':''" @click="change(15)">京东配送</view>
					<view :class="post.eliteId==24?'on':''" @click="change(24)">数码家电</view>
					<view :class="post.eliteId==25?'on':''" @click="change(25)">超市</view>
					<view :class="post.eliteId==26?'on':''" @click="change(26)">母婴玩具</view>
					<view :class="post.eliteId==27?'on':''" @click="change(27)">家具日用</view>
					<view :class="post.eliteId==28?'on':''" @click="change(28)">美妆穿搭</view>
					<view :class="post.eliteId==29?'on':''" @click="change(29)">医药保健</view>
					<view :class="post.eliteId==30?'on':''" @click="change(30)">图书文具</view>
					<view :class="post.eliteId==31?'on':''" @click="change(31)">今日必推</view>
					<view :class="post.eliteId==32?'on':''" @click="change(32)">京东好物</view>
				</view>
				
				<!-- banner -->
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#FF7B8E">
					<block v-for="(item,index) in sliderData.mainImg">
						<swiper-item>
							<image :src="item.url" ></image>
						</swiper-item>
					</block>
				</swiper>
				
			</view>
		</view>
		<view class="f5Bj-H20"></view>
		
		
		<view class="font-30 pt-4 d-flex j-center a-center colorM font-w line-h">
			<image src="../../static/images/home-icon1.png" class="icon"></image>
			<view class="px-3">今日推荐</view>
			<image src="../../static/images/home-icon.png" class="icon"></image>
		</view>
		
		<view class="mx-3 py-4 d-flex bB-e1" v-for="(item,index) in mainData" :key="index">
			<view class="position-relative">
				<image :src="item.imageInfo.imageList[0].url" class="wh250 rounded10"></image>
				<view class="tgTag">推广赚{{item.commissionInfo.commission}}</view>
			</view>
			<view class="d-flex flex-column pl-2" style="height: 250rpx;">
				<view class="font-30 flex-1 mb-2 avoidOverflow2">{{item.skuName}}</view>
				<view class="line-h color6 font-24">{{item.comments}}条评论 推广率{{item.goodCommentsShare}}%</view>
				<view class="line-h py-3 color6" style="padding-top:25rpx">
					<text class="colorR pr-2">券后价￥{{item.priceInfo.lowestPrice}}</text>
					<text class="font-24">京东价￥{{item.priceInfo.price}}</text>
				</view>
				<view class="line-h d-flex a-center font-26 colorf" style="line-height: 44rpx;">
					<!-- <view class="position-relative mr-2 text-center" style="height: 44rpx;width: 120rpx;">
						<image src="../../static/images/car-icon3.png" mode="widthFix"></image>
						<view class="position-absoluteXY pr-1">100元券</view>
					</view> -->
					<view class="Mbg d-flex a-center rounded px-1" @click="addCar(index)"> 
						<image src="../../static/images/car-icon.png" class="wh20"></image>
						<view>直播推广</view>
					</view>
					<view style="margin-left: 20rpx;color:#E81B1B">佣金比例{{item.commissionInfo.commissionShare}}%</view>
				</view>
			</view>
		</view>
		
		
		
		<view style="height: 130rpx;"></view>
		<view class="footer" :style="isIphoneX?'padding-bottom: 60rpx;padding-top: 20rpx;height:auto':''">
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
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
				Router:this.$Router,
				is_show: false,
				post:{
					eliteId:23,
					pageIndex:1,
				},
				mainData:[],
				sliderData:{},
				showAll:false
			}
		},
		
		onLoad(options) {
			const self = this;
			self.cartArray = self.$Utils.getStorageArray('cartData');
			console.log('self.cartArray',self.cartArray)
			self.$Utils.loadAll(['getMainData','getSliderData','getUserData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.post.pageIndex++;
				self.getMainData()
			};
		},
		
		methods: {
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
						if(self.userData.parent_no==''){
							self.Router.redirectTo({route:{path:'/pages/invitation-code/invitation-code'}})
							//self.showAll = true
						}else{
							self.showAll = true
						}
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			addCar(index) {
				const self = this;
				var obj = self.mainData[index];
				if(self.cartArray.length>0&&obj.commissionInfo.commissionShare!=self.cartArray[0].commissionInfo.commissionShare){
					uni.showModal({
						title:'提示',
						content:'您只可以添加相同返佣比例的商品至购物车，当前购物车选定返佣比例为:'+self.cartArray[0].commissionInfo.commissionShare+'%',
						showCancel:false,
						confirmText:'我知道了',
						success(res) {
							if(res.confirm){
								
							}
						}
					});
					return
				};
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].skuId == self.mainData[index].skuId) {
						var target = array[i]
					}
				};
				
				console.log(target)
				if (target) {
					target.count = target.count + 1
				} else {
					console.log(111)
					var target = self.mainData[index];
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('已加入购物车', 'none');
				self.$Utils.setStorageArray('cartData', target, 'skuId', 999);
				self.cartArray = self.$Utils.getStorageArray('cartData');
			},
			
			change(id){
				const self = this;
				if(self.post.eliteId!=id){
					self.post.eliteId = id;
					self.getMainData(true)
				}
			},
			
			getMainData(isNew) {
				const self = this;
				if(isNew){
					self.mainData = [];
					self.post.pageIndex = 1
				};
				const postData = self.post;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					};
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.searchProduct(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'首页轮播'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data[0]
					};
					self.$Utils.finishFunc('getSliderData');
			
				};
				self.$apis.labelGet(postData, callback);
			},
			
			
		}
	};
</script>
<style scoped>
.ss-icon{width: 29rpx;height: 29rpx;}
.ss{height: 60rpx;border-radius: 30rpx;background-color: #fff;}
input{flex: 1;background-color: #fff;font-size: 24rpx;}
.list{overflow-x: auto;}
.list view{margin-right: 30rpx;flex-shrink: 0;}
.list view:last-child{margin-right: 0;}
.list .on{position: relative;font-weight: bold;}
.list .on::before{content: '';background-color: #fff;width: 36rpx;height: 6rpx;border-radius: 5rpx;position: absolute;bottom: -15rpx;left: 50%;margin-left: -18rpx;}
swiper,swiper-item,swiper image{height: 300rpx;}

.icon{width: 174rpx;height: 13rpx;}
.colorR{color: #E81B1B;}
.tgTag{line-height: 44rpx;padding: 0 15rpx;background-color: rgba(0,0,0,0.4);color: #FFF;position: absolute;top: 0;left: 0;border-radius: 10rpx 0 10rpx 0;}
</style>
