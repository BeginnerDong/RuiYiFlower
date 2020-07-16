<template>
	<view class="line-h color2">
		<!-- banner -->
		<view class="banner p-r">
			<view class="back mt-3" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/back-icon.png" mode=""></image>
			</view>
			<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#FF6F48">
				<block>
					<swiper-item class="swiper-item">
						<image src="../../static/images/detailsl-img.png" class="slide-image" />
					</swiper-item>
				</block>
			</swiper>
		</view>
		
		<view class="bg-white p-3 d-flex j-sb mb-2">
			<view class="font-w">
				<view class="font-32 pb-4">LOVE礼盒系列·生生不息的爱</view>
				<view class="font-30 price">36.0</view>
			</view>
			<view class="text-center">
				<view class="font-24 color6 d-flex pl-3 bL-f5"><image src="../../static/images/detailsl-icon.png" class="fx-icon"></image>分享</view>
				<view class="font-22 color9 pt-5 pl-3">销量:255</view>
			</view>
		</view>
		
		<view class="bg-white px-3 mb-2">
			<view class="pt-3 pb-4 bB-f5 d-flex a-center">
				<view class="font-28 color6">配送</view>
				<view class="font-24 color2 d-flex">
					<view class="pl-3 d-flex"><image src="../../static/images/detailsl-icon1.png" class="ps-icon"></image>送货上门</view>
					<view class="pl-3 d-flex"><image src="../../static/images/detailsl-icon1.png" class="ps-icon"></image>到店自提</view>
				</view>
			</view>
			<view class="py-3 d-flex a-center">
				<view class="font-28 color6">配送</view>
				<view class="font-24 color2 pl-3">送货上门，需运费￥10 到店自提，免费</view>
			</view>
		</view>
		
		<view class="p-3 d-flex a-center bg-white mb-2">
			<view class="font-28 color6">规格</view>
			<view class="font-24 color2 flex-1 d-flex j-sb pl-3" @click="ggShow">
				<view class="flex-1">请选择</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
		</view>
		
		<view class="p-3 bg-white mb-2">
			<view class="font-28 color6 pb-3">养花技巧</view>
			<view class="font-24 color2 line-h-md">
				技巧技巧技巧技巧技巧技巧
			</view>
		</view>
		
		<view class="p-3 bg-white pb-5 ms">
			<view class="font-28 color6 pb-3">商品描述</view>
			<view class="font-24 color2 line-h-md text-center">
				<view>描述描述描述描述描述描述描述描述描述描述</view>
				<image src="../../static/images/detailsl-img1.png" mode=""></image>
			</view>
		</view>
		
		<view style="height: 100rpx;"></view>
		<view class="text-center colorf font-30 p-f bottom-0 left-0 right-0 d-flex bT-f5">
			<view class="flex-1 bg-white pt-2" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/detailsl-icon3.png" class="fh-icon"></image>
				<view class="font-24 color6 pt-1">首页</view>
			</view>
			<view class="btn">加入购物车</view>
			<view class="btn">立即购买</view>
		</view>
		
		<!-- 规格 -->
		<view class="bg-mask line-h" v-show="gg_show">
			<view class="radius20-T bg-white p-a bottom-0 left-0 right-0 p-3 d-flex flex-column ggBox">
				<view class="d-flex j-sb bB-f5 pb-3">
					<view class="gg"><image src="../../static/images/the orderl-img1.png"></image></view>
					<view class="pl-2 flex-1">
						<view class="font-36 price pb-3">69</view>
						<view class="font-24 color9">请选择规格</view>
					</view>
					<view @click="ggShow">
						<image src="../../static/images/detailsl-icon4.png" class="x-icon"></image>
					</view>
				</view>
				
				<view class="flex-1 flexY flex-column mb-3 ggPartBox">
					<view class="ggPart bB-f5 pb-1">
						<view class="font-26 color2 py-3">订几个月</view>
						<view class="font-24 color6">
							<view class="span on">1个月4束</view>
							<view class="span">3个月12束</view>
							<view class="span">6个月24束</view>
							<view class="span">12个月48束</view>
						</view>
					</view>
					<view class="ggPart pb-1">
						<view class="font-26 color2 py-3">配送星期</view>
						<view class="font-24 color6">
							<view class="span on">周一收花</view>
							<view class="span">周六收花</view>
						</view>
					</view>
				</view>
				
				<view class="font-30 colorf text-center d-flex pb-3">
					<view class="radiusL-4 ggBtn">加入购物车</view>
					<view class="radiusR-4 ggBtn">立即购买</view>
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
				gg_show:false
			}
		},
		methods: {
			ggShow(){
				const self = this;
				self.gg_show = !self.gg_show
			}
		}
	}
</script>

<style scoped>
.banner .swiper-box{width: 750rpx;height: 750rpx;}
.banner image{width: 750rpx;height: 750rpx;}

.ms image{width: 100%;height: 400rpx;margin-top: 40rpx;}

.fh-icon{width: 42rpx;height: 33rpx;margin: auto;}
.btn{width: 280rpx;line-height: 100rpx;background-color: #333;}
.btn:nth-child(2){background-color: #FF6740;}

.ggBox{min-height: 900rpx;}
.gg{width: 182rpx;}
.gg image{width: 182rpx;height: 182rpx;border-radius: 5rpx;position: absolute;top: -60rpx;}
.span{background-color: #f5f5f5;padding: 10rpx 20rpx;margin-right: 30rpx;margin-bottom: 20rpx;display: inline-block;}
.ggPart .on{background-color: #FDF7F5;color: #FF6740;border: 1px solid #FF6740;}
.ggBtn{line-height: 80rpx;background-color: #333;width: 345rpx;}
.ggBtn:nth-child(2){background-color: #FF6740;}
.ggPartBox{max-height: 600rpx;}
</style>
