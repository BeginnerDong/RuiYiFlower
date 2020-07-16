<template>
	<view>
		
		<view class="bg-white py-3 px-2 mx-3 my-2 radius10 overflow-h line-h d-flex a-center j-sb p-r mb-2">
			<view class="font-26">
				<view class="pb-3 color9">客户信息</view>
				<view>张三 15684279536</view>
			</view>
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a top-0 left-0 right-0"></image>
		</view>
		
		<view class="p-2 d-flex a-center j-sb bg-white mx-3">
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
		
		
		<view class="btnBox">
			<view class="btn690">确认核销</view>
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
.shopCon .tit{width: 455rpx;}
.btnBox{padding-top: 220rpx;}
</style>
