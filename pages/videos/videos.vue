<template>
	<view class="videos">
		<video :autoplay="true" :loop="true" :show-mute-btn="true" src="../../static/yeshengaoteman.mp4"></video>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
  .videos {
		height: 1250rpx;
		width: 750rpx;
		video {
			width: 100%;
			height: 100%;
		}
	}
</style>
