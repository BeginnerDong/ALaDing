<template>
	<view class="bg-white px-3 font-28">
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6 flex-1">头像</view>
			<image src="../../static/images/the login-icon.png" class="wh80"></image>
			<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">直播名称</view>
			<input type="text" value="" placeholder="请输入" />
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">擅长品类</view>
			<view class="flex" @click="isShow">
				<view class="font-24 color9">请选择(可多选)</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">直播平台</view>
			<view class="flex" @click="isShow">
				<view class="font-24 color9">请选择</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">客单价</view>
			<input type="text" value="" placeholder="请输入" />
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">直播名称</view>
			<input type="text" value="" placeholder="请输入" />
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">粉丝量</view>
			<view class="flex" @click="isShow">
				<view class="font-24 color9">请选择</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">女性粉丝占比</view>
			<view class="flex" @click="isShow">
				<view class="font-24 color9">请选择</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">所属机构</view>
			<view class="flex" @click="isShow">
				<view class="font-24 color9">请选择(可多选)</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		
		
		<view class="py-4 borderB-f5">
			<view class="submit" >确定</view>
		</view>
		
		
		<view class="bg-mask" v-show="is_show">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(v,i) in 3" :key="i" @click="changeLi(i)">
						<view>不限</view>
						<image src="../../static/images/the host-icon4.png" class="yes-icon" v-show="liCurr==i"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="isShow">确定</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				is_show:false,
				liCurr:0
			}
		},
		
		onLoad() {
			const self = this;
		},
		
		methods: {
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			},
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
		}
	}
</script>
<style scoped>
input{font-size: 24rpx;text-align: right;}
input::-webkit-input-placeholder{color: #999!important;}
.chooseBox{margin: 20% 75rpx;height: 800rpx;}
</style>
