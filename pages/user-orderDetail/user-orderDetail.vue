<template>
	<view>
		<view class="bg-white py-3 px-2 mx-3 mt-2 radius10 overflow-h line-h d-flex a-center j-sb p-r mb-2">
			<!-- 核销显示 -->
			<view class="font-26">
				<view class="pb-3">收件人：张三 15684279536</view>
				<view class="colorR pb-3">门店名称</view>
				<view class="color6 pb-3">地址：陕西省西安市雁塔区高新大都荟</view>
				<view class="color6">电话：15682348596</view>
			</view>
			<!-- 包月、快递订单显示 -->
			<!-- <view class="font-26">
				<view class="pb-3">张三 15684279536</view>
				<view>陕西省西安市长安区韦曲街道</view>
			</view> -->
			
			
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a top-0 left-0 right-0"></image>
		</view>
		
		<view class="bg-white mx-3 px-2 mt-2">
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
			<!-- 自提订单显示 -->
			<view class="d-flex a-center j-sb py-3 bT-f5">
				<view>提货码：</view>
				<image src="../../static/images/the orderl-img2.png" class="hx-icon"></image>
			</view>
		</view>
		<view class="bg-white mx-3 px-2 mt-2">
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
			<!-- 自提订单显示 -->
			<view class="d-flex a-center j-sb py-3 bT-f5">
				<view>提货码：</view>
				<image src="../../static/images/the orderl-img2.png" class="hx-icon"></image>
			</view>
		</view>
		
		<view class="bg-white mx-3 radius10 mt-2 font-24 color9 px-2 pb-3">
			<view class="flex1 py-3 bB-f5 color2 mb-3">
				<view>共1件商品</view>
				<view>合计：<text class="price font-28">38.6</text></view>
			</view>
			<view class="pb-3">支付方式：<text class="colorR">线下支付</text></view>    <!-- 包月订单显示 -->
			<view class="pb-3">订单编号：26598465368798435156</view>
			<view>下单时间：2019.12.23 11:02:25</view>
		</view>
		
		<view class="bg-white mx-3 radius10 mt-2 font-28 color2 px-2 pb-3">
			<view class="py-3">退款原因</view>
			<view class="font-26 color6">原因原因原因原因原因原因原因原因原因原因原因原因原因</view>
		</view>
		
		<view style="height: 50rpx;"></view>
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
</style>
 