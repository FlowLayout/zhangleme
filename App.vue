<script>
	export default {
		onLaunch: function() {
			//console.log('App Launch')
		},
		onShow: function() {
			uni.navigateTo({
				url:"pages/index/index"
			})
			setTimeout(()=>{uni.navigateBack()},2400)
			//console.log('App Show')
		},
		onHide: function() {
			//console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import url("@/static/My.css");
</style>
