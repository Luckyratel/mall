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

<style lang="scss">
	/*每个页面公共css */
	@import "uview-ui/index.scss";
	@import  url("static/iconfont/iconfont.css");
	page{
		height: 100%;
		width: 100%;
		background: #F0F0F0;
	}
</style>
