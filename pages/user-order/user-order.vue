<template>
	<view>
		
		<view class="font-26 color2 mx-3 my-2 bg-white d-flex overflow-h orderList">
			<view class="orderLi" :class="orderLiCurr==0?'on':''" @click="changeOrderLi(0)">门店自提</view>
			<view class="orderLi bL-f5 bR-f5" :class="orderLiCurr==1?'on':''" @click="changeOrderLi(1)">送货上门</view>
			<view class="orderLi" :class="orderLiCurr==2?'on':''" @click="changeOrderLi(2)">包月订单</view>
		</view>
		
		<!-- 自提门店 -->
		<view v-show="orderLiCurr==0">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li1" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
				<view class="li li1" :class="liCurr==1?'on':''" @click="changeLi(1)">待提货</view>
				<view class="li li1" :class="liCurr==2?'on':''" @click="changeLi(2)">已提货</view>
				<view class="li li1" :class="liCurr==3?'on':''" @click="changeLi(3)">退款售后</view>
			</view>
			
			<!-- 待提货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：2659784265898595</view>
					<view class="Mcolor">待提货</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5">
					<view class="d-flex a-center">
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon m-2" @click="Router.redirectTo({route:{path:'/pages/user-orderDetail/user-orderDetail'}})"></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">2018.12.23 11:00:03</view>
					<view>供3件商品 合计：￥56</view>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="d-flex a-center">
						<view>提货码：</view>
						<image src="../../static/images/the orderl-img2.png" class="hx-icon"></image>
					</view>
					<view class="tkBtn b-e1 radius10" @click="Router.redirectTo({route:{path:'/pages/user-refund/user-refund'}})">申请退款</view>
				</view>
			</view>
			
			<!-- 已提货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：2659784265898595</view>
					<view class="Mcolor">已提货</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5">
					<view class="d-flex a-center">
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon m-2" @click="Router.redirectTo({route:{path:'/pages/user-orderDetail/user-orderDetail'}})"></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">2018.12.23 11:00:03</view>
					<view>供3件商品 合计：￥56</view>
				</view>
			</view>
			
		</view>
		
		<!-- 送货上门 -->
		<view v-show="orderLiCurr==1">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li2" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
				<view class="li li2" :class="liCurr==1?'on':''" @click="changeLi(1)">待送货</view>
				<view class="li li2" :class="liCurr==2?'on':''" @click="changeLi(2)">送货中</view>
				<view class="li li2" :class="liCurr==3?'on':''" @click="changeLi(3)">已完成</view>
				<view class="li li2" :class="liCurr==4?'on':''" @click="changeLi(4)">退款售后</view>
			</view>
			
			<!-- 已发货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：2659784265898595</view>
					<view class="Mcolor">已发货</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5">
					<view class="d-flex a-center">
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
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
					<view class="tkBtn b-e1 radius10">申请退款</view>
				</view>
			</view>
			
			<!-- 已收货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：2659784265898595</view>
					<view class="Mcolor">已收货</view>
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
			</view>
			
		</view>
		
		<!-- 包月订单 -->
		<view v-show="orderLiCurr==2">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li3" :class="liCurr==0?'on':''" @click="changeLi(0)">全部</view>
				<view class="li li3" :class="liCurr==1?'on':''" @click="changeLi(1)">待送货</view>
				<view class="li li3" :class="liCurr==2?'on':''" @click="changeLi(2)">送货中</view>
			</view>
			
			<!-- 已收货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：2659784265898595</view>
					<view class="Mcolor">已收货</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5">
					<view class="d-flex a-center">
						<image src="../../static/images/shopping-img.png" class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">2018.12.23</view>
					<view>供3件商品 合计：￥56</view>
				</view>
			</view>
			
		</view>
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				orderLiCurr:0,
				liCurr:0
			}
		},
		methods: {
			changeOrderLi(i){
				const self = this;
				self.orderLiCurr = i
			},
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
		}
	}
</script>

<style>
.orderList{line-height: 70rpx;border-radius: 35rpx;}
.orderLi{width: 33.33%;text-align: center;}
.orderList .on{background-color: #FF6740;color: #fff;}

.li1{width: 25%;}
.li2{width: 20%;}
.li3{width: 33.33%;}

.orderImg{width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.tkBtn{width: 140rpx;line-height: 54rpx;text-align: center;}
</style>
