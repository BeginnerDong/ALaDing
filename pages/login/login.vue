<template>
	<view>
		
		<view class="position-relative">
			<image src="../../static/images/thelogin-img1.png" class="loginBg"></image>
			<image src="../../static/images/thelogin-img.png" class="nameImg"></image>
		</view>
		
		<view class="mx65 d-flex a-start">
			<image src="../../static/images/thelogin-icon.png" class="dh-icon mr-3"></image>
			<input type="text" value="" placeholder="输入手机号码" v-model="phone"/>
		</view>
		<view class="mx65 d-flex a-start">
			<image src="../../static/images/thelogin-icon1.png" class="aq-icon mr-3"></image>
			<input type="text" value="" placeholder="输入验证码" v-model="code"/>
			<button class="btn2" @click="sendCode()" v-if="!hasSend" style="background-color:#ff7b8e;color: #fff;border-radius: 10rpx;margin: 0;">{{text}}</button>
			<button class="btn2" style="background-color:#ff7b8e;color: #fff;border-radius: 10rpx;margin: 0;" v-else>{{text}}</button>
		</view>
		
		<view class="btn600" @click="userInfoUpdate">确定</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				phone:'',
				code:'',
				currentTime:61,
				text:'获取验证码',
				hasSend:false,
			}
		},
		methods: {
			
			
			sendCode(){
				var self = this;
				console.log(111)
				if(self.hasSend){
					return;
				};
				var phone = self.phone;
				if (phone.trim().length != 11 || !/^1[3|4|5|6|7|8|9]\d{9}$/.test(phone)) {
					self.$Utils.showToast('请输入正确的手机号', 'none', 1000)
					return;
				}
				var postData = {
					data:{
						thirdapp_id:2,
						phone:self.phone,
					}
				};
				var callback = function(res){
					if(res.solely_code==100000){
						uni.setStorageSync('canClick',true);
						uni.hideLoading();
						self.hasSend = true;
						var interval = setInterval(function() {
							self.currentTime--; //每执行一次让倒计时秒数减一
						
							self.text=self.currentTime + 's';//按钮文字变成倒计时对应秒数
							
							//如果当秒数小于等于0时 停止计时器 且按钮文字变成重新发送 且按钮变成可用状态 倒计时的秒数也要恢复成默认秒数 即让获取验证码的按钮恢复到初始化状态只改变按钮文字
							if (self.currentTime <= 0) {
								clearInterval(interval)
								
								self.hasSend = false;
								self.text='重新发送';
								self.currentTime= 61;
								
							}
							
						}, 1000);
					}else{
						uni.hideLoading();
						self.$Utils.showToast('发送失败', 'none', 1000)
					};
				};
				self.$apis.codeGet(postData, callback);
			},
			
			userInfoUpdate(){
				const self = this;
				if(self.phone==''){
					self.$Utils.showToast('请输入手机号','none');
					return
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					phone:self.phone
				};
				postData.smsAuth = {
					phone:self.phone,						
					code:self.code
				};
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('登录成功','none');
						setTimeout(function() {
							self.Router.redirectTo({route:{path:'/pages/user/user'}})
						}, 1000);	
					}else{
						self.$Utils.showToast(res.msg, 'none');
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
.loginBg{height: 338rpx;}
.nameImg{width: 244rpx; height: 77rpx;position: absolute;top: 0;left: 0;right: 0;bottom: 0;margin: auto;}
.dh-icon{width: 29rpx;height: 43rpx;}
.aq-icon{width: 36rpx;height: 40rpx;margin-left: -4rpx;}
input{height: 64rpx;font-size: 24rpx;flex: 1;border-bottom: 1px solid #e1e1e1;}
.mx65{margin-left: 65rpx;margin-right: 65rpx;margin-top: 60rpx;}
.btn600{margin: 100rpx auto;}
</style>
