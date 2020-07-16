<template>
	<view>
		
		<view class="bg-white mx-3 px-2 my-2">
			<view class="py-3 d-flex a-center j-sb">
				<image src="../../static/images/shopping-img.png" class="shopImg"></image>
				<view class="shopCon d-flex flex-column">
					<view class="tit avoidOverflow pb-2">哼唱幸福 11枝粉色扶郎花束</view>
					<view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view>
					<view class="flex1">
						<view class="price">38.6</view>
						<view class="font-26 color6">x1</view>
					</view>
				</view>
			</view>
		</view>
		
		<textarea value="" placeholder="请写出退款原因" />
		
		<view class="btn690">确定</view>
		
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

<style>
.shopCon .tit{width: 455rpx;}
textarea{width: 690rpx;height: 400rpx;background: #fff;padding: 30rpx 20rpx;box-sizing: border-box;font-size: 26rpx;margin: 0 30rpx 80rpx;border-radius: 10rpx;}
</style>
