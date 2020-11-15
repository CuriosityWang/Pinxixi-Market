<template>
	<view class="goods_list">
		<view class="goods_item" @click="clickInfo(item.id)" v-for="item in goods" :key="item.id" >
			<view class="goods_pic">
				<image :src="item.img_url"></image>
			</view>
			<view class="goods_price">
				<text class="after_discount">￥{{item.sell_price}}</text>
				<text class="before_discount">￥{{item.market_price}}</text>
			</view>
			<view class="goods_name">{{item.title}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ["goods"],
		data() {
			return {
				
			}
		},
		methods: {
			clickInfo(id){
				uni.navigateTo({
					url:"../goods-detail/goods-detail?goodsid=" + id
				})
			}
			
		},
	}
</script>

<style lang="scss">
	.goods_list{
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.goods_item{
			background-color: #fff;
			width: 355rpx;
			margin: 10rpx 0;
			box-sizing: border-box;
			padding: 15rpx;
			image{
				width: 70%;
				height: 150px;
				display: block;
				margin: 0 auto;
			}
		}
		.goods_price{
			color: $shop-color;
			font-size: 35rpx;
			.before_discount{
				color: #CCC;
				font-size: 28rpx;
				margin-left: 10rpx;
				text-decoration: line-through;//让文字中间有斜线
			}
		}
		.goods_name{
			font-size: 28rpx;
			line-height: 50rpx;
			padding-bottom: 15rpx;
			padding-bottom: 10rpx;
			}
	}
</style>
