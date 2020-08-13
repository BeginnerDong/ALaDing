<template>
	<view class="bg-white px-3 font-28">
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6 flex-1">头像</view>
			<image :src="submitData.mainImg.length>0?submitData.mainImg[0].url:'../../static/images/the login-icon.png'"
			 @click="upLoadImg('mainImg')" class="wh80"></image>
			<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">直播名称</view>
			<input type="text" value="" placeholder="请输入" v-model="submitData.name"/>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">擅长品类</view>
			<view class="flex" @click="isShow('good')">
				<view class="font-24 color9">{{submitData.goodAt!=''?submitData.goodAt:'请选择(可多选)'}}</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">直播平台</view>
			<view class="flex" @click="isShow('plant')">
				<view class="font-24 color9">{{submitData.anchorPlant!=''?submitData.anchorPlant:'请选择(可多选)'}}</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">客单价</view>
			<input type="text" value="" placeholder="请输入" v-model="submitData.orderPrice"/>
		</view>
		
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">粉丝量</view>
			<input type="text" value="" placeholder="请输入(单位/万)" v-model="submitData.fansCount"/>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">男性粉丝占比</view>
			<view class="flex" @click="isShow('male')">
				<view class="font-24 color9">{{submitData.manFansPercent!=''?submitData.manFansPercent:'请选择'}}</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">女性粉丝占比</view>
			<view class="flex" @click="isShow('famale')">
				<view class="font-24 color9">{{submitData.womenFansPercent!=''?submitData.womenFansPercent:'请选择'}}</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		<view class="py-4 borderB-f5 d-flex a-center j-sb">
			<view class="color6">所属机构</view>
			<view class="flex" @click="isShow('institute')">
				<view class="font-24 color9">{{submitData.institute!=''?submitData.institute:'请选择(可多选)'}}</view>
				<image src="../../static/images/the host-icon2.png" class="R-icon ml-1"></image>
			</view>
		</view>
		
		
		<view class="py-4 borderB-f5">
			<view class="submit" @click="submit">确定</view>
		</view>
		
		
		<view class="bg-mask" v-show="is_show.good">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in goodAtData" :key="index" @click="choose(item,'chooseGoodArray')">
						<view>{{item}}{{Utils.inArray(item,chooseGoodArray)}}</view>
						<image :src="Utils.inArray(item,chooseGoodArray)>-1?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="goodConfirm()">确定</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="is_show.plant">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in plantData" :key="index" @click="choose(item,'choosePlantArray')">
						<view>{{item}}{{Utils.inArray(item,choosePlantArray)}}</view>
						<image :src="Utils.inArray(item,choosePlantArray)>-1?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="plantConfirm()">确定</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="is_show.plant">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in plantData" :key="index" @click="choose(item,'choosePlantArray')">
						<view>{{item}}{{Utils.inArray(item,choosePlantArray)}}</view>
						<image :src="Utils.inArray(item,choosePlantArray)>-1?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="plantConfirm()">确定</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="is_show.male">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in rateData" :key="index" @click="sigleChoose(index,'maleRate')">
						<view>{{item}}</view>
						<image :src="maleRate==item?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="maleConfirm()">确定</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="is_show.famale">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in rateData" :key="index" @click="sigleChoose(index,'famaleRate')">
						<view>{{item}}</view>
						<image :src="famaleRate==item?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="famaleConfirm()">确定</view>
			</view>
		</view>
		
		<view class="bg-mask" v-show="is_show.institute">
			<view class="bg-white rounded10 d-flex flex-column overflow-h chooseBox">
				<view class="flexY flex-1">
					<view class="flex1 font-26 py-4 bB-e1 px-3" v-for="(item,index) in instituteData" :key="index" @click="choose(item,'chooseInstituteArray')">
						<view>{{item}}{{Utils.inArray(item,chooseInstituteArray)}}</view>
						<image :src="Utils.inArray(item,chooseInstituteArray)>-1?'../../static/images/the host-icon4.png':''" class="yes-icon"></image>
					</view>
				</view>
				
				<view class="py-3 colorf text-center Mbg" @click="instituteConfirm()">确定</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				liCurr:0,
				submitData:{
					name:'',
					goodAt:'',
					anchorPlant:'',
					orderPrice:'',
					fansCount:'',
					manFansPercent:'',
					womenFansPercent:'',
					institute:'',
					mainImg:[]
				},
				goodAtData:[],
				plantData:[],
				instituteData:[],
				rateData:[],
				is_show:{
					good:false,
					plant:false,
					male:false,
					famale:false,
					institute:false
				},
				currentShow:'',
				Utils:this.$Utils,
				chooseGoodArray:[],
				choosePlantArray:[],
				chooseInstituteArray:[],
				
				maleRate:'',
				famaleRate:''
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getGoodAtData','getPlantData','getRateData','getInstituteData'], self);
		},
		
		methods: {
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				var newObject = self.$Utils.cloneForm(self.submitData);
				const pass = self.$Utils.checkComplete(newObject);
				console.log('self.submitData',self.submitData)
				if (pass) {	
					self.userInfoUpdate();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全所有信息', 'none')
				};
			},
			
			upLoadImg(type) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type] = [];
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log(self.submitData)
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 1,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths[0];
						var file = res.tempFiles[0];
						var obj = res.tempFiles[0].path.lastIndexOf(".");
						var ext = res.tempFiles[0].path.substr(obj+1);
						console.log(callback)
						self.$Utils.uploadFile(tempFilePaths, 'file', {
							tokenFuncName: 'getProjectToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
						}, callback)
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
			sigleChoose(index,name){
				const self = this;
				self[name] = self.rateData[index]
			},
			
			maleConfirm(){
				const self = this;
				self.submitData.manFansPercent = self.maleRate;
				self.is_show.male = false
			},
			
			
			
			famaleConfirm(){
				const self = this;
				self.submitData.womenFansPercent = self.famaleRate;
				self.is_show.famale = false
			},
			
			plantConfirm(){
				const self = this;
				if(self.choosePlantArray.length>0){
					self.submitData.anchorPlant = self.choosePlantArray.join(',')
				};
				console.log('submitData',self.submitData);
				self.is_show.plant = false
			},
			
			goodConfirm(){
				const self = this;
				if(self.chooseGoodArray.length>0){
					self.submitData.goodAt = self.chooseGoodArray.join(',')
				};
				console.log('submitData',self.submitData);
				self.is_show.good = false
			},
			
			instituteConfirm(){
				const self = this;
				if(self.chooseInstituteArray.length>0){
					self.submitData.institute = self.chooseInstituteArray.join(',')
				};
				console.log('submitData',self.submitData);
				self.is_show.institute = false
			},
			
			choose(item,arrayName){
				const self = this;
				var options = self[arrayName].indexOf(item);
				console.log('options',options)
				if(options>=0){
					self[arrayName].splice(options,1)
				}else{
					self[arrayName].push(item)
				}
				console.log('self[arrayName]',self[arrayName])
			},
			
			isShow(type,status){
				const self = this;
				self.currentShow = type;
				self.is_show[type] = !self.is_show[type];
			},
			
			changeLi(i){
				const self = this;
				self.liCurr = i
			},
			
			getInstituteData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'所属机构'
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
						//self.instituteData = res.info.data[0].child;
						for (var i = 0; i < res.info.data[0].child.length; i++) {
							self.instituteData.push(res.info.data[0].child[i].title)
						}
					};
					self.$Utils.finishFunc('getInstituteData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getRateData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'粉丝占比'
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
							self.rateData.push(res.info.data[0].child[i].title)
						}
					};
					self.$Utils.finishFunc('getRateData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getPlantData() {
				const self = this;
				const postData = {
					searchItem:{
						title:'直播平台'
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
							self.plantData.push(res.info.data[0].child[i].title)
						}
					};
					self.$Utils.finishFunc('getPlantData');
				};
				self.$apis.labelGet(postData, callback);
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
			
			userInfoUpdate(){
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = self.$Utils.cloneForm(self.submitData)
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('完善成功','none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
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
input{font-size: 24rpx;text-align: right;}
input::-webkit-input-placeholder{color: #999!important;}
.chooseBox{margin: 20% 75rpx;height: 800rpx;}
</style>
