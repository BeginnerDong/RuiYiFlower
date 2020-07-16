<template>
	<view class="color2 font-32">
		<view class="mb-2 bg-white px-3 pb-3">
			<view class="d-flex j-sb font-w py-3">
				<view><text class="colorR">100</text>元套餐</view>
				<image src="../../static/images/shopping-icon.png" class="shop-icon"></image>
			</view>
			<view class="d-flex j-sb font-24 text-center">
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-icon6.png" class="rechImg"></image>
						<view class="p-aXY colorf line-h">
							<view class="rechPrice py-2">10</view>
							<view>满100可用</view>
						</view>
					</view>
					<view class="py-2">优惠券</view>
				</view>
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-img1.png" class="rechImg"></image>
					</view>
					<view class="py-2">向阳花10束</view>
				</view>
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-img1.png" class="rechImg"></image>
					</view>
					<view class="py-2">向阳花10束</view>
				</view>
			</view>
		</view>
		<view class="mb-2 bg-white px-3 pb-3">
			<view class="d-flex j-sb font-w py-3">
				<view><text class="colorR">100</text>元套餐</view>
				<image src="../../static/images/shopping-icon1.png" class="shop-icon"></image>
			</view>
			<view class="d-flex j-sb font-24 text-center">
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-icon6.png" class="rechImg"></image>
						<view class="p-aXY colorf line-h">
							<view class="rechPrice py-2">10</view>
							<view>满100可用</view>
						</view>
					</view>
					<view class="py-2">优惠券</view>
				</view>
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-img1.png" class="rechImg"></image>
					</view>
					<view class="py-2">向阳花10束</view>
				</view>
				<view class="rech borderM radius10">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-img1.png" class="rechImg"></image>
					</view>
					<view class="py-2">向阳花10束</view>
				</view>
			</view>
		</view>
		
		
		
		
		<view style="height: 180rpx;"></view>
		<view class="bg-white py-4 p-f bottom-0 left-0 right-0">
			<view class="btn690">立即支付</view>
		</view>
		
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

<style scoped>
.rechTop{width: 208rpx;height: 150rpx;background-color: #FDF7F5;box-sizing: border-box;}
.rechImg{width: 190rpx;height: 130rpx;}
.rechPrice{font-size: 40rpx;font-family: 'Impact';}
.rechPrice::before{content: '￥';font-size: 16rpx;font-weight: 800;}
</style>
