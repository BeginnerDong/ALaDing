<template>
	<view>
		<view class="list px-3 bg-white">
			<view class="listLi d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/about-usl-icon.png" mode=""></image>
				<view class="color6 font-28 pl-2 flex-1">客服微信</view>
				<view class="color2 font-26">{{mainData.description}}</view>
			</view>
			<view class="listLi d-flex a-center py-3 borderB-f5">
				<image src="../../static/images/about-usl-icon1.png" mode=""></image>
				<view class="color6 font-28 pl-2 flex-1">联系电话</view>
				<view class="color2 font-26">{{mainData.small_title}}</view>
			</view>
			<view class="listLi d-flex a-start py-3 borderB-f5">
				<image src="../../static/images/about-usl-icon2.png" mode=""></image>
				<view class="color6 font-28 pl-2 flex-1">公司地址</view>
				<view class="color2 font-26 dz">{{mainData.passage1}}</view>
			</view>
		</view>
		<view class="fg"></view>
		
		<view class="aboutBox px-3">
			<view class="content ql-editor" style="padding:0;" v-html="mainData.content">
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
							title: ['in', ['关于我们']],
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


<style>
.fg{width: 100%;height: 20rpx;background-color: #f5f5f5;}

.listLi image{width: 50rpx;height: 50rpx;}
.dz{width: 400rpx;text-align: right;}

.aboutBox image{width: 690rpx;height: 400rpx;}
</style>
