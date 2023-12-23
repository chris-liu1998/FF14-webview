<template>
	<view>
		<web-view src="https://ff.web.sdo.com/ff14risingstones/mob/index.html"></web-view>
	</view>
</template>
<script>
	var wv;
	export default {
		data() {
			return {
				canBack: false
			};
		},
		onLoad(){
			
		},
		onReady() {
			var self = this;
			var currentWebview = this.$scope.$getAppWebview();
			setTimeout(function() {
				wv = currentWebview.children()[0];
				wv.addEventListener(
					'progressChanged',
					function(e) {
						wv.canBack(function(e) {
							self.canBack = e.canBack;
						});
					},
					false
				);
			}, 1000);
		},
		onBackPress(e) {
			if (this.canBack) {
				wv.back();
				return true;
			}
			return false;
		}
	};
</script>