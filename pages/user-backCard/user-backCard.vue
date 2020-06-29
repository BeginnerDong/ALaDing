<template>
	<view class="bg-white pb-4">
		<view class="line-h px-3">
			<view class="d-flex j-sb a-center py-4 borderB-f5">
				<view class="color2 font-28">开户人姓名</view>
				<input type="text" maxlength="4" placeholder="请输入" v-model="submitData.bank_name" class="color9 font-22 text-right"/>
			</view>
			<view class="d-flex j-sb a-center py-4 borderB-f5">
				<view class="color2 font-28">开户人电话</view>
				<input type="number"  maxlength="11" placeholder="请输入" v-model="submitData.bank_phone" class="color9 font-22 text-right"/>
			</view>
			<view class="d-flex j-sb a-center py-4 borderB-f5">
				<view class="color2 font-28">开户行</view>
				<input type="text"  placeholder="请输入" v-model="submitData.bank" class="color9 font-22 text-right"/>
			</view>
			<view class="d-flex j-sb a-center py-4 borderB-f5">
				<view class="color2 font-28">开户账号</view>
				<input type="number"  placeholder="请输入" v-model="submitData.card_no" class="color9 font-22 text-right"/>
			</view>
		</view>
		
		<view class="submit mx-3 mt-4" @click="Utils.stopMultiClick(submit)">确定</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				submitData:{
					bank:'',
					card_no:'',
					bank_name:'',
					bank_phone:''
				},
				userInfoData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getUserInfoData'], self);
		},
		
	
		methods: {
			
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('self.submitData',self.submitData)
				if (pass) {
					 
					if(!/^[\u4E00-\u9FA5]+$/.test(self.submitData.bank)){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请输入正确的开户行', 'none');
						return
					}
					self.userInfoUpdate();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			

			getUserInfoData() {
				const self = this;
				const postData = {};
				
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no: uni.getStorageSync('userInfo').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0];
						self.submitData.bank = self.userInfoData.bank;
						self.submitData.card_no = self.userInfoData.card_no;
						self.submitData.bank_name = self.userInfoData.bank_name;
						self.submitData.bank_phone = self.userInfoData.bank_phone;
					};
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
		
			
			userInfoUpdate() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no: uni.getStorageSync('userInfo').user_no
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				const callback = (data) => {				
					if (data.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.userInfoUpdate(postData, callback);
			},

		},
	};
</script>


<style>
page{background-color: #f5f5f5;}
</style>
