<template>
	<view class="goods_list">
		<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		<view class="isOver" v-if="flag">----我是有底线的----</view>
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
				pageindex: 1,
				goods: [],
				flag: false
			}
		},
		onLoad() {
			this.getGoodsList()
		},
		methods: {
			// 获取商品列表的数据
			async getGoodsList(callBack) {
				const res = await this.$http({
					url: '/api/getgoods?pageindex=' + this.pageindex
				})
				this.goods = [...this.goods, ...res.data.message]
				callBack && callBack()
			},
			// 导航到商品详情页
			goGoodsDetail(id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id=' + id
				})
			}
		},
		// 上拉加载更多
		onReachBottom() {
			if(this.goods.length < this.pageindex * 10) return this.flag = true
			this.pageindex++
			this.getGoodsList()
		},
		// 下拉刷新功能
		onPullDownRefresh() {
			console.log('下拉刷新了')
			this.pageindex = 1
			this.goods = []
			this.flag = false
			this.getGoodsList(() => {
				uni.stopPullDownRefresh()
			})
		}
	}
</script>

<style lang="scss">
  .goods_list {
		background: #eee;
	}
	.isOver {
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
	}
</style>
