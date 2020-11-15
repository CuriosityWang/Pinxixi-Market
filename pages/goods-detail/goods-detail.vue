<template>
	<view class="home">
		<swiper indicator-dots="true">
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.src"></image>
			</swiper-item>
		</swiper>
		
		<view class="box1">
			<view class="price">
				<text class="after_discount">￥{{gooodsProperty.sell_price}}</text>
				<text class="before_discount">￥{{gooodsProperty.market_price}}</text>
			</view>
			<view class="title">{{gooodsProperty.title}}</view>
		</view>
		
		<view class="box2">
			<view>货号:  {{gooodsProperty.goods_no}}</view>
			<view class="inventory">库存:  {{gooodsProperty.stock_quantity}}</view>
		</view>
		
		<view class="box3">
			<view class="intro">详细介绍:</view>
			<rich-text class="richText" :nodes="introduction.content"></rich-text>
		</view>
		<uni-goods-nav class="goodsnav" :fill="true"  :options="options" :buttonGroup="buttonGroup"  @click="onClick" @buttonClick="buttonClick" />
	</view>
	
</template>

<script>
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		components: {uniGoodsNav},
		data() {
			return {
				id: 0,
				swipers: [],
				introduction: [],
				gooodsProperty: [],
				options: [{
					icon: 'headphones',
					text: '客服'
					}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor:'#007aff',
					infoColor:"red"
					}, {
					icon: 'cart',
					text: '购物车',
					info: 3
					}],
					buttonGroup: [{
					text: '加入购物车',
					backgroundColor: '#ff0000',
					color: '#fff'
					},
					{
					  text: '立即购买',
					  backgroundColor: '#ffa200',
					  color: '#fff'
					}
				]
			}
		},
		methods: {
			onLoad(options){
				this.id = options.goodsid
				this.getSwipers()
				this.getIntroduction()
			},
			
			async getSwipers() {
				const res = await this.$myRequest({
					url : "/api/getthumimages/" + this.id
				})
				this.swipers = res.data.message
			},
			
			async getIntroduction() {
				//得到商品的详细介绍
				const res_1 = await this.$myRequest({
					url : "/api/goods/getdesc/" + this.id
				})
				this.introduction = res_1.data.message[0]
				
				//得到商品的属性 价格 名称 货号 库存等
				const res_2 = await this.$myRequest({
					url : "/api/goods/getinfo/" + this.id
				})
				this.gooodsProperty = res_2.data.message[0]		
			},
			onClick (e) {
				// console.log(e)
				if(e.index == 0)
				{
					uni.showToast({
						title:"客服页面暂未开发"
					})
				}
				if(e.index == 1)
				{
					uni.showToast({
						title:"店铺页面暂未开发"
					})
				}
				if(e.index == 2)
				{
		
				}
				
			  },
			  
			buttonClick (e) {
				console.log(e)
				this.options[2].info++
			  }
		}
	}
</script>

<style lang="scss">
	.home{
		background-color: #BEBEBE;
		swiper{
			background: #FFF;
			width: 750rpx;
			height: 700rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
	}
	
	.box1{
		background-color: #fff;
		padding-top: 10px;
		margin-bottom: 3px;
		.price{
			color: $shop-color;
			font-size: 40rpx;
			.before_discount{
				color: #CCC;
				font-size: 35rpx;
				margin-left: 10rpx;
				text-decoration: line-through;//让文字中间有斜线
			}
		};
		.title{
			font-size: 35rpx;
			line-height: 60rpx;
		}
	}
	
	.box2{
		background-color: #fff;
		margin-bottom: 3px;
		view{
			line-height: 70rpx;
			font-size: 35rpx;
		}
		
	}
	
	.box3{
		background-color: #fff;
		padding-top: 10px;
		margin-bottom: 5px;
		view{
			line-height: 60rpx;
			font-size: 32rpx;
		}
		.richText{
			line-height: 60rpx;
			font-size: 32rpx;
			
		}
	}
	.goodsnav{
		position: fixed;
		bottom: 0;
		width: 100%;
	}
</style>
