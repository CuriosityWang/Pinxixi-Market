<template>
	<view>
		<view class="swiper">
			<swiper indicator-dots="true" circular="true" class="test">
				<swiper-item v-for="item in swipers" :key="item.id">
					<image :src="item.img"></image>
				</swiper-item>
			</swiper>
		</view>
		
		<!-- 导航区域 -->
		<view class="nav">
			<view class="iconpic" v-for="(item,index) in navs" :key="index">
			</view>
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navTo(item.path)">
				<view><image :src="item.icon_url"></image></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="goods_title">
				推荐商品
			</view>
			<GoodsList :goods="hotgoods" @myEvent="getGoodsdetail"></GoodsList>
		</view>
	</view>
</template>

<script>
	import GoodsList from "../../components/good-list/good-list.vue"
	
	export default {
		data() {
			return {
				swipers: [],
				hotgoods: [],
				goodsid: 0,
				navs: [
					{
						icon_url: "/static/icon/shop.png",
						title: '拼夕夕超市',
						path: '/pages/goods/goods'
					},
					{
						icon_url: "/static/icon/contact.png",
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon_url: "/static/icon/pci.png",
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon_url: "/static/icon/vde.png",
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				],
			}
		},
		
		onLoad() {
			this.getSwipers()
			this.getHotgoods()
		},
		
		components:{GoodsList},
		methods: {
			//获取轮播图数据
			async getSwipers() {
				const res = await this.$myRequest({
					url : "/api/getlunbo"
				})
				this.swipers = res.data.message
			},
			
			//获取热门商品数据
			async getHotgoods() {
				const res = await this.$myRequest({
					url:'/api/getgoods?pageindex=1'
				})
				this.hotgoods = res.data.message
			},
			//导航跳转函数
			navTo(url){
				uni.navigateTo({
					url,
				})
			},
			
			//接收子组件传来的 newsid
			getGoodsdetail(res){
				uni.navigateTo({
					url:"../goods-detail/goods-detail?id=" + res
				})
			}
		}
	}
</script>

<style lang="scss">
	swiper{
		width: 750rpx;
		height: 380rpx;
		image{
			width: 100%;
			height: 100%;
		}
	}
	
	.nav{
		margin-top: 8rpx;
		display: flex;
		.iconpic{
			image{
				height: 110rpx;
				width: 110rpx;
				margin: 0 auto;
			}
		}
		image{
			height: 110rpx;
			width: 110rpx;
			margin: 0 auto;
		}
		.nav_item{
			width: 25%;
			text-align: center;
			text{
				font-size: 30rpx;
			}
		}
	}
	.hot_goods{
		background: #eee;
		margin-top: 10rpx;
		overflow: hidden;
		.goods_title{
			height: 100rpx;
			line-height: 100rpx;
			color: $shop-color;
			text-align: center;
			letter-spacing: 20rpx;//行距
			background-color: #fff;
			margin: 7rpx 0;
		}
	}
	
	
</style>
