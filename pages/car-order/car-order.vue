<template>
	<view class="color2 font-28">
		<view class="bg-white bB-f5">
			<view class="px-3 py-2 d-flex orderList">
				<view class="orderLi borderM radiusL" :class="orderLiCurr==0?'on':''" @click="changeOrderLi(0)">到店自提</view>
				<view class="orderLi borderM radiusR" :class="orderLiCurr==1?'on':''" @click="changeOrderLi(1)">送货上门</view>
			</view>
		</view>
		<view class="bg-white line-h p-r pb-1 mb-2">
			<view class="p-3 line-h d-flex a-center j-sb p-r" @click="Router.redirectTo({route:{path:'/pages/user-store/user-store'}})">
				<view>
					<view class="pb-3">张三 15684279536</view>
					<view>陕西省西安市长安区韦曲街道</view>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
			<view class="flex1 px-3 font-24 text-center pb-2 zt" v-show="orderLiCurr==0">
				<input type="text" value="" placeholder="姓名" />
				<input type="text" value="" placeholder="电话" />
			</view>
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a bottom-0 left-0 right-0"></image>
		</view>
		
		<view class="bg-white px-3 mb-2">
			<view class="py-3 d-flex a-center j-sb bB-f5">
				<image src="../../static/images/shopping-img.png" class="shopImg"></image>
				<view class="shopCon d-flex flex-column">
					<view class="tit avoidOverflow pb-2">哼唱幸福 11枝粉色扶郎花束</view>
					<view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view>
					<view class="price">38.6</view>
				</view>
			</view>
			<view class="d-flex a-center j-sb py-3">
				<view>购买数量</view>
				<view class="b-e1 d-flex a-center count">
					<image src="../../static/images/shopping-icon2.png" class="count-icon1"></image>
					<view class="num bL-e1 bR-e1 text-center">1</view>
					<image src="../../static/images/shopping-icon3.png" class="count-icon2"></image>
				</view>
			</view>
		</view>
		
		<view class="bg-white px-3">
			<view class="py-3 bB-f5 flex1">
				<view>运费</view>
				<view class="font-24 color6">快递费￥0</view>
			</view>
			<view class="py-3 flex1">
				<view>支付方式</view>
				<view class="font-24 flex0">
					<image src="../../static/images/shopping-icon.png" class="shop-icon"></image>
					<view class="pl-1">立即支付</view>
				</view>
			</view>
		</view>
		
		
		
		<view class="bg-white p-f left-0 right-0 d-flex carBot">
			<view class="font-22 d-flex a-center flex-1 px-3">合计 <text class="price font-30">79</text></view>
			<view class="carBtn" @click="Router.redirectTo({route:{path:'/pages/car-order/car-order'}})">确认订单</view>
		</view>
		
		
		<!-- 充值免费领弹窗 -->
		<!-- <view class="bg-mask">
			<view class="exec p-aXY m-a bg-white radius20 font-30 color2 flex5 pb-5">
				<view class="py-5">充值免费领</view>
				<image src="../../static/images/img.png" class="lb"></image>
				<view class="btn690">立即充值</view>
				<image src="../../static/images/detailsl-icon4.png" class="x-icon p-a top-0 right-0 m-3"></image>
			</view>
		</view> -->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				orderLiCurr:0
			}
		},
		methods: {
			changeOrderLi(i){
				const self = this;
				self.orderLiCurr = i
			}
		}
	}
</script>

<style>
.orderList{line-height: 60rpx;border-radius: 10rpx;}
.orderLi{width: 50%;text-align: center;}
.orderList .on{background-color: #FF6740;color: #fff;}

.zt input{width: 335rpx;line-height: 50rpx;border: 1px solid #e1e1e1;border-radius: 5rpx;height: 50rpx;}

.shopImg{width: 183rpx;height: 183rpx;}
.shopCon .tit{width: 490rpx;}
.carSpan{background-color: #FDF7F5;line-height: 36rpx;}

.carBot{bottom: 0;}

.exec{width: 600rpx;height: 660rpx;}
.lb{width: 251rpx;height: 305rpx;}
.btn690{width: 480rpx;margin: 0;}

.R-icon{margin: 30rpx;margin-right: 0;}
</style>
