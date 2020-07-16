<template>
	<view>
		<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">待提货</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">已提货</view>
		</view>
		
		<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="color6">订单编号：2659784265898595</view>
				<view class="Mcolor">已提货</view>
			</view>
			<view class="d-flex j-sb a-center p-2 bB-f5">
				<view class="d-flex a-center">
					<image src="../../static/images/shopping-img.png" class="orderImg"></image>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="color9">2018.12.23 11:00:03</view>
				<view>供3件商品 合计：￥56</view>
			</view>
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="d-flex a-center">支付方式：线上支付</view>
				<view>张丹 15685475288</view>
			</view>
		</view>
		
		<image src="../../static/images/scanl-icon.png" class="sys" @click="Router.redirectTo({route:{path:'/pages/user-writeOffOrders/user-writeOffOrders'}})"></image>
		
		
		<view style="height: 120rpx;"></view>
		<view class="py-3 bT-f5 p-f bottom-0 left-0 right-0 text-center bg-white dis" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">退出登录</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				liCurr:0
			}
		},
		methods: {
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
		}
	}
</script>

<style>
.li{width: 33.33%;}
.orderImg{width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.tkBtn{width: 140rpx;line-height: 54rpx;text-align: center;}
.dis{height: 100rpx;}

.sys{width: 100rpx;height: 100rpx;position: fixed;top: 45%;right: 0;}
</style>
