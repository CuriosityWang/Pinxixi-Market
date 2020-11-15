<template>
	<view class="contact">
		<image src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="PhoneCall()"> 电话: 554-556-4952 (点击拨打)</view>
			<view> 邮箱: lightwxz@foxmail.com</view>
			<view> 地址: 山东省济南市山东师范大学长清湖校区</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude" scale="14" :markers="covers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 116.833577,
				latitude: 36.546481,
				 covers: [{
					longitude: 116.833577,
					latitude: 36.546481,
					iconPath: "../../static/icon/location.png",
					width: 15,
					height: 20
				}]
			}
		},
		methods: {
			PhoneCall(){
				uni.makePhoneCall({
					 phoneNumber: '5545564952'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact{
		image{
			width: 750rpx;
			height: 360rpx;
		}
		.info{
			padding-left: 15rpx;
			view{
				line-height: 100rpx;
				border-bottom: 1px #eee solid;
			}
		}
	}
	.map{
		width: 750rpx;
		height: 750rpx;
	}
</style>
