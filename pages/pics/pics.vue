<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view 
			@click="leftClickHandle(index,item.id)"
			:class="active===index?'active':''" 
			v-for="(item,index) in cates" 
			:key="item.id">
			  {{item.title}}
			</view>
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view v-for="item in rightDate" class="item">
				<image @click="preview(item.img_url)" :src="item.img_url"></image>
				<view class="title">{{item.title}}</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates: [],
				active: 0,
				rightDate: []
			}
		},
		methods: {
			async getPicsCate () {
				const res = await this.$myRequest({
					url: '/api/getimgcategory'
				})
				this.cates = res.data.message
			},
			async leftClickHandle (index,id) {
				this.active = index
				//获取右侧数据
				 const res = await this.$myRequest({
					url: "/api/getimages/" + id
				})
				this.rightDate = res.data.message
			},
			onLoad () {
				this.getPicsCate()
			},
			preview(current){
				const urls = this.rightDate.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					current,
					urls
				})
			}
		}
	}
</script>

<style lang="scss">
page{
	height: 100%;
}
.pics{
	height: 100%;
	display: flex;
	.left{
		width: 200rpx;
		height: 100%;
		border-right:1px solid #eee;
		view{
			height: 60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top:1px solid #eee;
		}
		.active{
			background: $shop-color;
			color: #fff;
		}
	}
	.right{
		width: 530rpx;
		margin: 10rpx auto;
		.item{
			border-radius: 5rpx;
		}
		.title{
			line-height: 50rpx;
			font-size: 30rpx;
			padding-bottom: 25rpx;
		}
	}
}
</style>
