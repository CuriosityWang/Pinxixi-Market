<template>
	<view class="test">
		<GoodsList :goods="goods"></GoodsList>
		<view class="bottom" v-if="flag">----我是有底线的----</view>
	</view>
</template>

<script>
	import GoodsList from "../../components/good-list/good-list.vue"
	export default {
		data() {
			return {
				pageindex: 1,
				goods: [],
				flag: false
			}
		},
		components: {GoodsList},
		methods: {
			async getGoodslist(){
				const res = await this.$myRequest({
					url:'/api/getgoods?pageindex=' + this.pageindex
				})
				this.goods = [...this.goods, ...res.data.message]
				uni.stopPullDownRefresh()
			}
		},
		onLoad() {
			this.getGoodslist()
		},
		onReachBottom() {
			if(this.goods.length%10 != 0) return this.flag = true
			uni.showLoading({
				title:"加载中...."
			})
			this.pageindex++
			this.getGoodslist()
			setTimeout(function () {
			    uni.hideLoading();
			}, 500);
		},
		
		onPullDownRefresh() {
			this.pageindex = 1
			this.flag = false
			this.goods = []
			setTimeout(()=> {
				this.getGoodslist()
			}, 1000);
		}
	}
</script>

<style lang="scss">
	.test{
		background-color: #eee;
	}
	.bottom{
		width: 100%;
		height: 50rpx;
		line-height: 50px;
		text-align: center;
		padding-bottom: 10px;
		font-size: 28rpx;
	}
</style>
