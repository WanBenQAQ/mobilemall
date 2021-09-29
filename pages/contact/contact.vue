<template>
	<view class="contact">
		<image class="img" src="https://tse1-mm.cn.bing.net/th/id/R-C.3a55b8738251f0003c6b89244dd667e9?rik=pjED6buOLryw0A&riu=http%3a%2f%2fwww.ytled.com.cn%2fimg%2fgywm.jpg%3fk%3d1590995791000&ehk=Oo5EjQxpHTHtk6AbmXd8ulG6evKpbzSC4GtJx%2fJhtI4%3d&risl=&pid=ImgRaw&r=0"></image>
	  <view class="info">
			<view @click="calPhone">联系电话：18299619516 ( 点击拨打 )</view>
			<view>联系地址：湖北省武汉市江夏区庙山街道武昌理工学院</view>
		</view>
		<map class="map" :longitude="longitude" :scale="scale" :latitude="latitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 114.36903,
				latitude: 30.417003,
				scale: 15,
				markers: [
					{
						longitude: 114.3703,
						latitude: 30.416503,
						iconPath: '../../static/wut.png',
						width: 30,
						height: 30
					}
				]
			}
		},
		methods: {
			calPhone() {
				uni.makePhoneCall({
					phoneNumber: '18299619516'
				})
			}
		}
	}
</script>

<style lang="scss">
  .contact {
		.img {
			width: 750rpx;
			height: 320rpx;
		}
		.info {
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view {
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map {
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
