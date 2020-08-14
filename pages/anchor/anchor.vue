<template>
	<view>
		
		<view class="px-3 py-2 Mbg">
			 <view class="bg-white rounded30 flex1 px-3">
				 <image src="../../static/images/the-host-icon.png" class="wh29 p-a mr-2"></image>
				 <input type="text" value="" placeholder="搜索" v-model="keywords" @confirm="search"/>
			 </view>
		</view>
		
		<!-- banner -->
		<view class="banner m-3">
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#FF7B8E">
				<block v-for="(item,index) in sliderData.mainImg" :key="index">
					<swiper-item>
						<image :src="item.url" ></image>
					</swiper-item>
				</block>
			</swiper>
		</view>
		
		<view class="font-30 font-w line-h px-3 pb-3 pt-2">优质主播推荐</view>
		<view class="font-24 line-h flex2 bB-f5 shadowB z-index10 nav">
			<view class="flex py-3" @click="Show(1)" :class="navCurr==1&&tj_show?'on':''">
				<view>擅长类型</view>
				<image src="../../static/images/the-host-icon3.png" class="sj-icon" v-if="navCurr==1&&tj_show"></image>
				<image src="../../static/images/the-host-icon1.png" class="sj-icon" v-else></image>
			</view>
			<view class="flex py-3" @click="Show(2)" :class="navCurr==2&&tj_show?'on':''">
				<view>粉丝数</view>
				<image src="../../static/images/the-host-icon3.png" class="sj-icon" v-if="navCurr==2&&tj_show"></image>
				<image src="../../static/images/the-host-icon1.png" class="sj-icon" v-else></image>
			</view>
			<view class="flex py-3" @click="Show(3)" :class="navCurr==3&&tj_show?'on':''">
				<view>客单价</view>
				<image src="../../static/images/the-host-icon3.png" class="sj-icon" v-if="navCurr==3&&tj_show"></image>
				<image src="../../static/images/the-host-icon1.png" class="sj-icon" v-else></image>
			</view>
		</view>
		
		<view class="px-3 py-1 position-relative">
			<!-- 导航弹框 -->
			<view class="anchor-mask" v-show="tj_show&&navCurr==1">
				<view class="px-3 bg-white rounded20-B">
					<view class="flex1 font-26 py-4 bB-e1" v-for="(item,index) in goodAtData" :key="index" @click="goodChoose(index)">
						<view>{{item}}</view>
						<image src="../../static/images/the-host-icon4.png" class="yes-icon" v-show="goodIndex==index"></image>
					</view>
				</view>
			</view>
			
			<view class="anchor-mask" v-show="tj_show&&navCurr==2">
				<view class="px-3 bg-white rounded20-B">
					<view class="flex1 font-26 py-4 bB-e1" v-for="(item,index) in fans" :key="index" @click="fansChoose(index)">
						<view>{{item.name}}</view>
						<image src="../../static/images/the-host-icon4.png" class="yes-icon" v-show="fansIndex==index"></image>
					</view>
				</view>
			</view>
			
			<view class="anchor-mask" v-show="tj_show&&navCurr==3">
				<view class="px-3 bg-white rounded20-B">
					<view class="flex1 font-26 py-4 bB-e1" v-for="(item,index) in price" :key="index" @click="priceChoose(index)">
						<view>{{item.name}}</view>
						<image src="../../static/images/the-host-icon4.png" class="yes-icon" v-show="priceIndex==index"></image>
					</view>
				</view>
			</view>
			
			<!-- 主播列表 -->
			<view class="flex1 py-3 bB-e1 anchor" v-for="(item,index) in mainData" v-if="mainData.length>0" :data-user_no="item.user_no"
			@click="Router.navigateTo({route:{path:'/pages/anchorDetail/anchorDetail?user_no='+$event.currentTarget.dataset.user_no}})" :key="index">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="anchorImg"></image>
				<view class="font-24 color6 pl-2 flex-1 flex5 py-1 anchorCon">
					<view class="flex">
						<view class="font-30 color2 font-w">{{item.name}}</view>
						<view class="tag" v-for="(c_item,c_index) in item.anchorPlant" :key="c_index">{{c_item}}</view>
						
					</view>
					<view>粉丝数量：{{item.fansCount}}万</view>
					<view>客单价：{{item.orderPrice}}元</view>
					<view>近3月直播：{{item.anchorSession}}场</view>
				</view>
				<image src="../../static/images/the-host-icon2.png" class="R-icon"></image>
			</view>
			<view style="width: 100%;text-align: center;margin-top: 50rpx;" v-if="mainData.length==0">暂时没有符合条件的主播~</view>
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
			<view class="item .on" @click="Router.redirectTo({route:{path:'/pages/anchor/anchor'}})">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
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
				tj_show:false,
				navCurr:0,
				liCurr:0,
				searchItem:{
					thirdapp_id:2,
					anchorPlant:['not in',['']]
				},
				goodAtData:[],
				mainData:[],
				sliderData:{},
				fans:[{name:'不限',type:'delete',value:[]},{name:'100-1000',type:'between',value:[100,1000]}
				,{name:'1000-5000',type:'between',value:[1000,5000]},{name:'5000-1万',type:'between',value:[5000,10000]},
				{name:'1万-10万',type:'between',value:[10000,100000]},{name:'10万以上',type:'higher',value:100000}],
				price:[{name:'不限',type:'delete',value:[]},{name:'10-40元',type:'between',value:[10,40]}
				,{name:'40-60元',type:'between',value:[40,60]},{name:'60-100元',type:'between',value:[60,100]},
				{name:'100-1000元',type:'between',value:[100,1000]},{name:'1000元以上',type:'higher',value:1000}],
				goodIndex:-1,
				keywords:''
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getSliderData','getGoodAtData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')&&self.navCurr==0) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			search(){
				const self = this;
				if(self.keywords!=''){
					self.searchItem.name = ['like',['%'+self.keywords+'%']];
				}else{
					delete self.searchItem.name
				};
				self.getMainData(true)
			},
			
			fansChoose(index){
				const self = this;
				if(self.fansIndex!=index){
					if(self.fans[index].type=='delete'&&self.searchItem.fansCount){
						delete self.searchItem.fansCount
					}else if(self.fans[index].type=='higher'){
						self.searchItem.fansCount = ['>',self.fans[index].value]
					}else if(self.fans[index].type=='between'){
						self.searchItem.fansCount = ['between',self.fans[index].value]
					};
					self.tj_show = false;
					self.navCurr = 0;
					self.getMainData(true)
				}
			},
			
			priceChoose(index){
				const self = this;
				if(self.priceIndex!=index){
					if(self.price[index].type=='delete'&&self.searchItem.orderPrice){
						delete self.searchItem.orderPrice
					}else if(self.price[index].type=='higher'){
						self.searchItem.orderPrice = ['>',self.price[index].value]
					}else if(self.price[index].type=='between'){
						self.searchItem.orderPrice = ['between',self.price[index].value]
					};
					self.tj_show = false;
					self.navCurr = 0;
					self.getMainData(true)
				}
			},
			
			goodChoose(index){
				const self = this;
				if(self.goodIndex!=index){
					self.goodIndex = index;
					self.searchItem.goodAt = ['like',['%'+self.goodAtData[self.goodIndex]+'%']];
					self.tj_show = false;
					self.navCurr = 0;
					self.getMainData(true)
				}
			},
			
			getGoodAtData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'擅长品类'
					}
				};
				postData.getAfter = {
					child:{
						tableName:'Label',
						middleKey:'id',
						key:'parentid',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						for (var i = 0; i < res.info.data[0].child.length; i++) {
							self.goodAtData.push(res.info.data[0].child[i].title)
						}
					};
					self.$Utils.finishFunc('getGoodAtData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'主播轮播'
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
			
			Show(i){
				const self = this;
				if(self.navCurr != i){
					self.tj_show = true;
					self.navCurr = i
				}else{
					self.tj_show = false;
					self.navCurr = 0
				}
				
			},
			changeLi(i){
				const self = this;
				self.liCurr = i
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.getBefore = {
					user:{
						tableName:'User',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							behavior:['in',[1]]
						},
						condition:'in'
					}
				};
				postData.getAfter = {
					log:{
						tableName:'Log',
						middleKey:'user_no',
						key:'user_no',
						searchItem:{
							status:1,
							user_type:0
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
						
						
						for (var i = 0; i < self.mainData.length; i++) {
							self.mainData[i].anchorSession = 0;
							for (var j = 0; j < self.mainData[i].log.length; j++) {
								self.mainData[i].anchorSession += parseInt(self.mainData[i].log[j].anchorSession)
							};
							self.mainData[i].anchorPlant = self.mainData[i].anchorPlant.split(',')
						}
					};
					console.log('self.mainData',self.mainData)
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.userInfoGet(postData, callback);
			},
		}
	}
</script>

<style scoped>
input{font-size: 24rpx;height: 60rpx;flex: 1;}
.banner swiper{width: 690rpx;height: 300rpx;}
.banner image{border-radius: 10rpx;}
.anchorImg{width: 150rpx;height: 180rpx;}
.anchorCon{height: 180rpx;}
.anchor:nth-child(1){border: none!important;}

.nav .on{color: #FF7B8E;}
.anchor-mask{position: absolute;left: 0;right: 0;background-color: rgba(0,0,0,0.4);z-index: 22222;padding-bottom: 300rpx;}
</style>
