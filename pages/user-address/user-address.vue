<template>
	<view class="line-h">
		
		<view class="font-28 color6 mb-2">
			<view class="bB-f5 py-3 px-3">
				<view class="pb-3"><text class="color2 pr-3">张三</text> 15684279536</view>
				<view>陕西省西安市长安区韦曲街道</view>
			</view>
			<view class="py-3 flex1 px-3">
				<view class="flex1">
					<image src="../../static/images/shopping-icon.png" class="shop-icon"></image>
					<!-- <image src="../../static/images/shopping-icon1.png" class="shop-icon"></image> -->
					<view class="pl-1">默认地址</view>
				</view>
				<view class="flex1">
					<view class="flex1">
						<image src="../../static/images/addressl-icon.png" class="add-icon"></image>
						<view>编辑</view>
					</view>
					<view class="flex1 ml-5">
						<image src="../../static/images/addressl-icon1.png" class="add-icon"></image>
						<view>删除</view>
					</view>
				</view>
			</view>
			<view class="f5-2"></view>
		</view>
		
		
		
		<view style="height: 120rpx;"></view>
		<view class="flex0 py-3 bT-f5 p-f bottom-0 left-0 right-0 addBot" @click="Router.redirectTo({route:{path:'/pages/user-addAddress/user-addAddress'}})">
			<image src="../../static/images/addressl-icon2.png" class="add-icon"></image>
			<view>新增地址</view>
		</view>
		
		
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
	page{background: #fff;}
.add-icon{width: 26rpx;height: 26rpx;margin-right: 10rpx;}
.addBot{height: 100rpx;}
</style>