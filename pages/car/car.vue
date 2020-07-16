<template>
	<view class="font-28 color2">
		<view class="d-flex j-sb p-3 bg-white bB-f5">
			<view>全部商品(2)</view>
			<view @click="isShow">{{is_show?'管理':'删除'}}</view>
		</view>
		
		<view class="p-3 bg-white d-flex a-center j-sb mb-2">
			<image src="../../static/images/shopping-icon.png" class="shop-icon"></image>
			<image src="../../static/images/shopping-img.png" class="shopImg"></image>
			<view class="shopCon d-flex flex-column">
				<view class="tit avoidOverflow pb-2">哼唱幸福 11枝粉色扶郎花束</view>
				<view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view>
				<view class="d-flex j-sb">
					<view class="price">38.6</view>
					<view class="b-e1 d-flex a-center count">
						<image src="../../static/images/shopping-icon2.png" class="count-icon1"></image>
						<view class="num bL-e1 bR-e1 text-center">1</view>
						<image src="../../static/images/shopping-icon3.png" class="count-icon2"></image>
					</view>
				</view>
			</view>
		</view>
		<view class="p-3 bg-white d-flex a-center j-sb mb-2">
			<image src="../../static/images/shopping-icon1.png" class="shop-icon"></image>
			<image src="../../static/images/shopping-img.png" class="shopImg"></image>
			<view class="shopCon d-flex flex-column">
				<view class="tit avoidOverflow pb-2">哼唱幸福 11枝粉色扶郎花束</view>
				<view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view>
				<view class="d-flex j-sb">
					<view class="price">38.6</view>
					<view class="b-e1 d-flex a-center count">
						<image src="../../static/images/shopping-icon2.png" class="count-icon1"></image>
						<view class="num bL-e1 bR-e1 text-center">1</view>
						<image src="../../static/images/shopping-icon3.png" class="count-icon2"></image>
					</view>
				</view>
			</view>
		</view>
		
		
		
		
		
		
		<view style="height: 140rpx;"></view>
		<view class="bg-white p-f left-0 right-0 d-flex carBot" v-if="is_show">
			<view class="font-26 d-flex a-center j-sb px-3 flex-1">
				<view class="d-flex a-center">
					<image src="../../static/images/shopping-icon1.png" class="shop-icon"></image>
					<view class="pl-1">全选</view>
				</view>
				<view class="font-22 d-flex a-center">合计 <text class="price font-30">79</text></view>
			</view>
			<view class="carBtn" @click="Router.redirectTo({route:{path:'/pages/car-order/car-order'}})">立即购买</view>
		</view>
		<view class="bg-white p-f left-0 right-0 d-flex a-center j-sb px-3 carBot" v-else>
			<view class="d-flex a-center">
				<image src="../../static/images/shopping-icon1.png" class="shop-icon"></image>
				<view class="pl-1 font-26">全选</view>
			</view>
			<view class="font-23 borderM radius30 deleteBtn">删除</view>
		</view>
		
		
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>分类</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/VIP/VIP'}})">
				<image src="../../static/images/nabar3.png" mode=""></image>
				<view>会员</view>
			</view>
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar5.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show:true
			}
		},
		methods: {
			isShow(){
				const self = this;
				self.is_show = !self.is_show
			}
		}
	}
</script>

<style scoped>
.shopImg{width: 183rpx;height: 183rpx;}
.shopCon{width: 438rpx;}
.shopCon .tit{width: 438rpx;}
.carSpan{background-color: #FDF7F5;line-height: 36rpx;}

.deleteBtn{width: 160rpx;line-height: 60rpx;text-align: center;color: #FF6740;height: 60rpx;}
.carBot{bottom: 110rpx;}
</style>
