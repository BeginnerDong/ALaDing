<script>
	import token from "./common/token.js"
	export default {
		onLaunch: function() {
			let self = this;
			console.log(222)
			wx.getSystemInfo({
				success: res => {
					let modelmes = res.model;
					if (modelmes.search('iPhone X') != -1) {
						wx.setStorageSync('isIphoneX', true)
					}else{
						wx.setStorageSync('isIphoneX', false)
					}
					wx.setStorageSync('modelmes', modelmes)
				}
			})
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/* 富文本样式 */
	@import "/assets/style/quill.css";


	/* 公共样式 */
	@import "/common/css/common.css";
	/* 公共样式 */
	@import "/common/css/main.css";
</style>
