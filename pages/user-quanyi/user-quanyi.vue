<template>
	<view>
		
		<view class="text-center position-relative">
			<image src="../../static/images/quanyi-img.png" class="qyBg"></image>
			
			<view class="position-absoluteXY line-h">
				<view class="txt1 c1 font-50 pb-2">{{mainData.title?mainData.title:''}}</view>
				<view class="c1 font-26">{{mainData.description?mainData.description:''}}</view>
				<view class="txt2 font-36 font-w">{{mainData.small_title?mainData.small_title:''}}</view>
				
				<view class="con">
					<view class="d-flex conTxt">
						<view class="content ql-editor" style="padding:0;" v-html="mainData.content">
						</view>
					</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>

	const app = getApp();
	export default {
		
		data() {
			return {
				Router: this.$Router,
				mainData: {},
				//statusBar: app.globalData.statusBar,
			}
		},

		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},

		methods: {

			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'menu_id',
						key: 'id',
						searchItem: {
							title: ['in', ['身份权益']],
						},
						condition: 'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style scoped>
.qyBg{height: 1335rpx;}
.c1{color: #CDBBA1;}
.txt1{margin-top: 227rpx;}
.txt2{color: #926C35;margin-top: 72rpx;}
.con{padding-top: 46rpx;}
.conTxt{margin: 68rpx 93rpx 0;}
.line70{line-height: 70rpx;}
</style>
