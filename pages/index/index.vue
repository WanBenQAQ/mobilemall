<template>
	<view class="home">
	  <swiper indicator-dots circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item, index) in navs" :key="index" @click="navItemClick(item.path)">
				<view class="nav_item_img1">
					<image :src="item.img"></image>
				</view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
		<!-- 推荐商品区域 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		components: {
			goodsList
		},
		data() {
			return {
				swipers: [],
				goods: [],
				navs: [
					{
						img: '../../static/fonts/caoshi.png',
						title: '专营超市',
						path: '/pages/goods/goods'
					},
					{
						img: '../../static/fonts/xiaoxi.png',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						img: '../../static/fonts/tupian.png',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						img: '../../static/fonts/shiping.png',
						title: '教学视频',
						path: '/pages/videos/videos'
					},
				]
			}
		},
		onLoad() {
        this.getSwipers()
				this.getHotGoods()
		},
		methods: {
      // 获取轮播图数据
			async getSwipers() {
				const res = await this.$http({
					url: '/api/getlunbo'
				})
				this.swipers = res.data.message
			},
			// 获取热门商品列表数据
			async getHotGoods() {
				const res = await this.$http({
					url: '/api/getgoods?pageindex=1'
				})
				this.goods = res.data.message
			},
			// 导航点击的处理函数
			navItemClick(url) {
				uni.navigateTo({
					url
				})
			},
			// 导航到商品详情页
			goGoodsDetail(id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id=' + id
				})
			}
		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			width: 750rpx;
			height: 380rpx;
			image {
				height: 100%;
				width: 100%;
			}
		}
		.nav {
			display: flex;
			.nav_item {
				width: 25%;
				text-align: center;
				view {
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60rpx;
					margin: 10px auto;
					line-height: 150rpx;
				}
				text {
					font-size: 30rpx;
				}
				image {
					height: 55rpx;
					width: 55rpx;
				}
			}
		}
		.hot_goods {
			background-color: #eee;
			overflow: hidden;
			margin-top: 10px;
			.tit {
				height: 100rpx;
				line-height: 100rpx;
				color: $shop-color;
				text-align: center;
				letter-spacing: 20px;
				background: #fff;
				margin: 7rpx 0;
			}
		}
	}
</style>
