<template>
	<view class="line-h position-relative pt-3">
		<view class="bg"></view>
		
		<view class="mx-3 bg-white rounded10 position-relative mt-5 shadow py-5 d-flex">
			<view class="text-center w-50 zb position-relative" @click="Router.navigateTo({route:{path:'/pages/user-teamList/user-teamList?id=1'}})">
				<view class="font-40 color2 pb-3 font-w">{{zhuboNum}}</view>
				<view class="font-24 color2">我的主播 ></view>
			</view>
			<view class="text-center w-50" @click="Router.navigateTo({route:{path:'/pages/user-teamList/user-teamList?id=2'}})">
				<view class="font-40 color2 pb-3 font-w">{{daoshiNum}}</view>
				<view class="font-24 color2">我的导师 ></view>
			</view>
		</view>
		
		<view class="teamBox1 px-3 bg-white">
			<view class="font-28 color2 pt-4">我的上级</view>
			<view class="item d-flex a-center py-3" v-for="(item,index) of highUserData" :key="item.id">
				<image style="border-radius: 50%;overflow: hidden;" :src="item.relationUser&&item.relationUser[0]?item.relationUser[0].headImgUrl:''" mode=""></image>
				<view class="font-26 pl-2">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">{{item.relationUser&&item.relationUser[0]?item.relationUser[0].nickname:''}}</view>
						<view class="sign2" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==2">导师</view>
						<view class="sign3" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==1">主播</view>
					</view>
					<view class="color6 d-flex a-center">
						<view>微信号：{{item.relationUser&&item.relationUser[0]&&item.relationUser[0].info
						&&item.relationUser[0].info.wechat!=''?item.relationUser[0].info.wechat:'暂未填写'}}</view>
						<view class="sign4 ml-2" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].info
						&&item.relationUser[0].info.wechat!=''" @click="getClipboardData(0,index)">复制</view>
					</view>
				</view>
			</view>
			<view style="font-weight: 700;width: 100%;text-align: center;" class="item d-flex a-center py-3 borderB-f5" 
			v-if="highUserData.length==0">
				<span>暂无数据</span>
			</view>
		</view>
		
		<view class="teamBox2 px-3 bg-white mt-2">
			<view class="font-28 color2 pt-4">今日数据</view>
			<view class="item d-flex a-center py-3 borderB-f5" v-if="mainData.length>0" v-for="(item,index) of mainData" :key="item.id">
				<image style="border-radius: 50%;overflow: hidden;" :src="item.relationUser&&item.relationUser[0]?item.relationUser[0].headImgUrl:''" mode=""></image>
				<view class="font-26 pl-2 flex-1 d-flex flex-column j-sb" style="min-height: 100rpx;">
					<view class="d-flex a-center">
						<view class="color2 pr-2">{{item.relationUser&&item.relationUser[0]?item.relationUser[0].nickname:''}}</view>
						<view class="sign2" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==2">导师</view>
						<view class="sign3" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==1">主播</view>
					</view>
					<!-- ---------添加--------- -->
					<view class="color6 d-flex a-center">
						<view v-if="userData.behavior==2">微信号：{{item.relationUser&&item.relationUser[0]&&item.relationUser[0].info
						&&item.relationUser[0].info.wechat!=''?item.relationUser[0].info.wechat:'暂未填写'}}</view>
						<view class="sign4 ml-2" @click="getClipboardData(1,index)">复制</view>
					</view>
					<!-- ---------------添加------------- -->
					<view class="color6">注册时间：{{item.create_time}}</view>
				</view>
				<view class="font-40 qj" :data-user_no="item.child_no"
				 @click="Router.navigateTo({route:{path:'/pages/user-dataDetails/user-dataDetails?user_no='+$event.currentTarget.dataset.user_no}})">></view>
			</view>
			<view style="font-weight: 700;width: 100%;text-align: center;" class="item d-flex a-center py-3 borderB-f5" v-if="mainData.length==0">
				<span>暂无数据</span>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				Router:this.$Router,
				searchItem:{
					thirdapp_id:2,
					level:1
				},
				mainData:[],
				highUserData:[],
				daoshiNum:0,
				zhuboNum:0,
				userData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.searchItem.parent_no = uni.getStorageSync('user_info').user_no;
			self.$Utils.loadAll(['getMainData','getHighUserData','getUserData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
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
						self.userData = res.info.data[0];
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			getClipboardData(type,index){
				const self = this;
				uni.setClipboardData({
				    data: type==0?self.highUserData[index].relationUser[0].info.wechat:self.mainData[index].relationUser[0].info.wechat,
				    success: function () {
				        console.log('success');
				    }
				});
			},
			
			getHighUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					child_no:uni.getStorageSync('user_info').user_no,
					level:1
				};
				postData.getAfter = {
					relationUser:{
						tableName:'User',
						middleKey:'parent_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.highUserData.push.apply(self.highUserData, res.info.data);
					};
					self.$Utils.finishFunc('getHighUserData');
				};
				self.$apis.distriGet(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				var now = new Date().getTime();
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
				postData.getAfter = {
					relationUser:{
						tableName:'User',
						middleKey:'child_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'=',
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
						for (var i = 0; i < self.mainData.length; i++) {
							if(self.mainData[i].relationUser[0].behavior==1){
								self.zhuboNum++
							}else if(self.mainData[i].relationUser[0].behavior==2){
								self.daoshiNum++
							}
						}
					};
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.distriGet(postData, callback);
			},
			
		}
	}
</script>

<style>
page{background-color: #f5f5f5;}
	
.bg{height: 200rpx;background-color: #FF7B8E;position: absolute;top: 0;width: 100%;}

.zb::before{content: '';height: 50rpx;border-left: 1px dashed #d5d5d5;position: absolute;right: 0;top: 50%;margin-top: -25rpx;}

.teamBox1{padding-top: 74rpx;margin-top: -74rpx;}
.teamBox1 .item image{width: 100rpx;height: 100rpx;}
.teamBox2 .item image{width: 100rpx;height: 100rpx;}

.qj{color: #D5D5D5;width: 100rpx;text-align: right;height: 100rpx;line-height: 100rpx;}
</style>
