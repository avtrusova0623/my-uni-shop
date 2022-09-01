<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
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
	/* 官方uni css */
	@import "@/common/uni.css";
	/* 第三方动画库 */
	@import "@/common/animate.css";
	/* 自定义图标库 */
	@import "@/common/icon.css";
	/* 基础ui库 */
	@import "@/common/ui-main.css";
	/*每个页面公共css */
	@import "@/common/common.css"
</style>
