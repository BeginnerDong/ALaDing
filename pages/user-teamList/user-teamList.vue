<template>
	<view>
		<view class="color2 font-30 d-flex a-center text-center head shadow z-index10">
			<view class="w-50 title position-relative" :class="titCurrent==1?'on':''" @click="changeTit(1)">主播</view>
			<view class="w-50 title position-relative" :class="titCurrent==2?'on':''" @click="changeTit(2)">导师</view>
		</view>
		<!-- 主播列表 -->
		<view class="teamListBox px-3 bg-white mt-3">
			<view class="item d-flex a-center py-3 borderB-f5" v-if="mainData.length>0" v-for="(item,index) of mainData" :key="item.id">
				<image style="border-radius: 50%;overflow: hidden;" :src="item.relationUser&&item.relationUser[0]?item.relationUser[0].headImgUrl:''" mode=""></image>
				<view class="font-26 pl-2 flex-1">
					<view class="d-flex a-center pb-3">
						<view class="color2 pr-2">{{item.relationUser&&item.relationUser[0]?item.relationUser[0].nickname:''}}</view>
						<view class="sign2" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==2">导师</view>
						<view class="sign3" v-if="item.relationUser&&item.relationUser[0]&&item.relationUser[0].bahavior==1">主播</view>
					</view>
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
				searchItem:{
					thirdapp_id:2,
				},
				mainData:[],
				Router:this.$Router,
				titCurrent:1,
				getBefore:{
					relationUser:{
						tableName:'User',
						middleKey:'child_no',
						key:'user_no',
						searchItem:{
							behavior:['in',[1]]
						},
						condition:'in',
					}
				}
			}
		},
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.searchItem.parent_no = uni.getStorageSync('user_info').user_no;
			self.$Utils.loadAll(['getMainData'], self);
			self.titCurrent = options.id;
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
			
			changeTit(i){
				const self = this;
				if(i!=self.titCurrent){
					self.titCurrent = i;
					self.getBefore = {
						relationUser:{
							tableName:'User',
							middleKey:'child_no',
							key:'user_no',
							searchItem:{
								behavior:['in',[i]]
							},
							condition:'in',
						}
					};
					self.getMainData(true)
				}
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
				postData.getBefore = self.$Utils.cloneForm(self.getBefore);
				postData.getAfter = {
					relationUser:{
						tableName:'User',
						middleKey:'child_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'in',
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					};
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.distriGet(postData, callback);
			},
		}
	}
</script>

<style>
.head{height: 90rpx;line-height: 90rpx;}
.head .on{color: #FF7B8E;font-weight: 700;}
.head .on::before{content:'';width: 30rpx;height: 4rpx;background-color: #FF7B8E;position: absolute;bottom: 0;left: 50%;margin-left: -15rpx;}

.teamListBox .item image{width: 100rpx;height: 100rpx;}
.qj{color: #D5D5D5;width: 100rpx;text-align: right;height: 100rpx;line-height: 100rpx;}
</style>
