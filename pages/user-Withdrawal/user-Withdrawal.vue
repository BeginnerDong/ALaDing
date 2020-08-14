<template>
	<view>
		<view class="box bg-white mx-3 shadow">
			<view class="line-h py-5 px-3 d-flex a-center j-sb head"  v-if="userInfoData.bank!=''">
				<view class="font-30 color2">到账银行卡</view>
				<view class="font-24 color2 d-flex"  
				@click="Router.navigateTo({route:{path:'/pages/user-backCard/user-backCard'}})">
				{{userInfoData.bank?userInfoData.bank:''}}（{{userInfoData.card_no?userInfoData.card_no:''}}）<view class="color9">></view></view>
			</view>
			
			<view class="line-h py-5 px-3 d-flex a-center j-sb head"  v-else>
				<view class="font-30 color2">到账银行卡</view>
				<view class="font-24 color2 d-flex"  @click="Router.navigateTo({route:{path:'/pages/user-backCard/user-backCard'}})">
					请添加<view class="color9">></view></view>
			</view>
			
			<view class="py-5 font-24 color2 px-3">提现金额</view>
			<view class="picBox mx-3 borderB-f5 d-flex">
				<view>￥</view>
				<input type="digit" maxlength="10" v-model="submitData.count"/>
			</view>
			<view class="font-24 color6 pt-3 pb-5 d-flex j-sb px-3">
				<view>本次可提现￥{{canWithdraw}}</view>
				<view style="color: #fed513;" @click="allCount">全部提现</view>
			</view>
			<button class="mt-5 submit mx-3"
			open-type="getUserInfo"  @getuserinfo="Utils.stopMultiClick(submit)">提现</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,	
				Utils:this.$Utils,
				mainData:{},
				userInfoData:{},
				submitData:{
					count:''
				},
				canWithdraw:0
			}
		},
		
		onLoad(options) {
			
		},
		
		onShow() {
			const self = this;
			self.canWithdraw = parseFloat(uni.getStorageSync('canWithdraw'));
			self.$Utils.loadAll(['getUserInfoData'], self);
		},
		
		methods: {
			
			allCount(){
				const self = this;
				self.submitData.count = self.canWithdraw
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(!self.userInfoData.bank){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请先绑定银行卡', 'none');
					return
				};
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('self.submitData',self.submitData)
				if (pass) {
					if(parseFloat(self.submitData.count)>parseFloat(self.canWithdraw)){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('余额不足', 'none');
						return
					};
					if(parseFloat(self.submitData.count)<=0){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请输入正确的金额', 'none');
						return
					};
					
					const callback = (user, res) => {
						self.flowLogAdd();
					};
					self.$Utils.getAuthSetting(callback);	
					
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请输入提现金额', 'none')
				};
			},
			
			flowLogAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken'
				if(!wx.getStorageSync('user_info')||!wx.getStorageSync('user_info').headImgUrl){
				  postData.refreshToken = true;
				};
				postData.data = {
					count:-self.submitData.count,
					thirdapp_id:2,
					status:1,
					trade_info:'提现',
					withdraw:1,
					withdraw_status:0,
					type:2,
					account:1
				};
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('提交成功', 'none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 800)
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.flowLogAdd(postData, callback);
			},
			
			
			getUserInfoData() {
				const self = this;
				console.log('852369')
				const postData = {
					searchItem:{}
				};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.userInfoData = res.info.data[0]
						self.userInfoData.card_no  = self.userInfoData.card_no.substr(self.userInfoData.card_no.length-4)		
					} else {
						self.$Utils.showToast(res.msg, 'none');
					};
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},

			

		},
	};
</script>

<style>
page{background-color: #f5f5f5;}
.box{height: 632rpx;margin-top: 200rpx;}
.box .head{background-color: #fafafa;}

.picBox{font-size: 60rpx;color: #222;position: relative;}
.picBox input{height: 100%;}
</style>
