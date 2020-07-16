<template>
	<view class="color2">
		<view class="p-r pt-4">
			<image src="../../static/images/about-icon13.png" class="userBg"></image>
			
			<view class="p-r bg-white line-h text-center mx-3 radius10">
				<view class="colorR money">256</view>
				<view class="font-26 pb-5">可用余额</view>
			</view>
		</view>
		
		<view class="mx-3 px-2 py-3 bg1 mt-2">明细</view>
		<view class="px-2 mx-3 bg-white line-h">
			<view class="d-flex a-start j-sb bB-f5  py-3">
				<view class="font-20 borderM radius Mcolor">充</view>
				<view class="flex-1 px-1">
					<view class="font-28 pb-2">充值</view>
					<view class="font-22 color9">2020.05.23</view>
				</view>
				<view class="font-28 colorR">+125</view>
			</view>
			<view class="d-flex a-start j-sb bB-f5  py-3">
				<view class="font-20 borderM radius Mcolor">充</view>
				<view class="flex-1 px-1">
					<view class="font-28 pb-2">充值</view>
					<view class="font-22 color9">2020.05.23</view>
				</view>
				<view class="font-28 colorR">+125</view>
			</view>
			<view class="d-flex a-start j-sb bB-f5  py-3">
				<view class="font-20 borderM radius Mcolor">充</view>
				<view class="flex-1 px-1">
					<view class="font-28 pb-2">充值</view>
					<view class="font-22 color9">2020.05.23</view>
				</view>
				<view class="font-28 colorR">+125</view>
			</view>
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

<style>
.userBg{width: 750rpx;height: 180rpx;position: absolute;top: 0;}
.money{font-size: 70rpx;font-weight: 800;padding: 60rpx 0 34rpx;}

.bg1{background: #FDF7F5;}
</style>
