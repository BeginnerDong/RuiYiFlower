<template>
	<view>
		<view class="add px-3 font-28 mb-4">
			<view class="flex1 py-4 bB-f5">
				<view>姓名</view>
				<input type="text" value="" placeholder="填写姓名" />
			</view>
			<view class="flex1 py-4 bB-f5">
				<view>手机号</view>
				<input type="text" value="" placeholder="填写手机号" />
			</view>
			<view class="flex1 py-4 bB-f5">
				<view>所在地区</view>
				<view class="flex1 font-22 color9">请选择<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image></view>
			</view>
			<view class="flex1 py-4 bB-f5">
				<view>详细地址</view>
				<input type="text" value="" placeholder="请填写" />
			</view>
			<view class="flex1 py-4 bB-f5">
				<view>详细地址</view>
				<!-- <image src="../../static/images/addressl-icon3.png" class="add-icon2"></image> -->
				<image src="../../static/images/addressl-icon4.png" class="add-icon2"></image>
			</view>
		</view>
		
		<view class="btn690">确定</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #fff;}
.add input{text-align: right;font-size: 22rpx;flex: 1;}
.add-icon2{width: 67rpx;height: 34rpx;}
</style>
