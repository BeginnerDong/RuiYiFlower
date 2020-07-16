<template>
	<view>
		<!-- banner -->
		<view class="banner radius20 overflow-h mx-3 mt-2">
			<view class="headBg p-a top-0 left-0 right-0"><image src="../../static/images/about-icon13.png" mode=""></image></view>
			<swiper class="swiper-box" indicator-dots="indicatorDots" autoplay="autoplay" interval="3000" indicator-active-color="#FF6F48">
				<block>
					<swiper-item class="swiper-item">
						<image src="../../static/images/home-banner.png" class="slide-image" />
					</swiper-item>
				</block>
				<block>
					<swiper-item class="swiper-item">
						<image src="../../static/images/home-banner.png" class="slide-image" />
					</swiper-item>
				</block>
			</swiper>
		</view>
		
		<!-- 金刚区 -->
		<view class="mx-3 d-flex j-sb a-end mt-3">
			<view class="d-flex flex-column a-center tt">
				<image src="../../static/images/home-icon.png" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">应季鲜花</view>
			</view>
			<view class="d-flex flex-column a-center tt">
				<image src="../../static/images/home-icon1.png" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">应季鲜花</view>
			</view>
			<view class="d-flex flex-column a-center tt">
				<image src="../../static/images/home-icon2.png" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">应季鲜花</view>
			</view>
			<view class="d-flex flex-column a-center tt">
				<image src="../../static/images/home-icon3.png" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">应季鲜花</view>
			</view>
			<view class="d-flex flex-column a-center tt">
				<image src="../../static/images/home-icon4.png" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">应季鲜花</view>
			</view>
		</view>
		
		<!-- 热门专区 -->
		<view class="line-h font-32 color2 mt-5 mb-3 mx-3 Tit">热卖专区</view>
		<view class="line-h flexX">
			<view class="p-r ml-3 flex-shrink" @click="Router.redirectTo({route:{path:'/pages/goodsDetail/goodsDetail'}})">
				<view class="font-22 colorf sgin">销量:255</view>
				<image src="../../static/images/home-img.png" class="hotImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow hotTit">郁金香</view>
				<view class="font-28 price">36.0</view>
			</view>
			<view class="p-r ml-3 flex-shrink">
				<view class="font-22 colorf sgin">销量:255</view>
				<image src="../../static/images/home-img.png" class="hotImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow tit">郁金香</view>
				<view class="font-28 price">36.0</view>
			</view>
			<view class="p-r ml-3 flex-shrink">
				<view class="font-22 colorf sgin">销量:255</view>
				<image src="../../static/images/home-img.png" class="hotImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow hotTit">郁金香</view>
				<view class="font-28 price">36.0</view>
			</view>
		</view>
		
		<!-- 新品推荐 -->
		<view class="line-h font-32 color2 mt-5 mb-3 mx-3 Tit">新品推荐</view>
		<view class="line-h flexX">
			<view class="p-r ml-3 flex-shrink">
				<view class="font-22 colorf sgin">销量:255</view>
				<image src="../../static/images/home-img1.png" class="newImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow newTit">郁金香</view>
				<view class="font-28 price">36.0</view>
			</view>
			<view class="p-r ml-3 flex-shrink">
				<view class="font-22 colorf sgin">销量:255</view>
				<image src="../../static/images/home-img1.png" class="newImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow newTit">郁金香</view>
				<view class="font-28 price">36.0</view>
			</view>
		</view>
		
		<!-- 包月鲜花 -->
		<view class="line-h font-32 color2 mt-5 mb-3 mx-3 Tit">包月鲜花</view>
		<view class="line-h">
			<view class="p-r ml-3 pb-5">
				<image src="../../static/images/home-img2.png" class="yueImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow yueTit">爱的味道 11枝香槟玫瑰混搭3枝多头百合花束</view>
				<view class="font-28 price">36.0</view>
			</view>
			<view class="p-r ml-3 pb-5">
				<image src="../../static/images/home-img2.png" class="yueImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow yueTit">爱的味道 11枝香槟玫瑰混搭3枝多头百合花束</view>
				<view class="font-28 price">36.0</view>
			</view>
		</view>
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
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
				is_show: false,
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>
<style>
.headBg image{height: 180rpx;}
.banner .swiper-box{width: 690rpx;height: 300rpx;}

.tt .icon{height: 100rpx;width: 112rpx;}
.tt:nth-child(2) .icon{height: 102rpx;width: 122rpx;}
.tt:nth-child(3) .icon{height: 105rpx;width: 111rpx;}
.tt:nth-child(4) .icon{height: 129rpx;width: 109rpx;}
.tt:nth-child(5) .icon{height: 100rpx;width: 102rpx;}

.Tit{position: relative;text-indent: 18rpx;}
.Tit::before {content: '';background-color: #FF6740;height: 20rpx;width: 10rpx;position: absolute;top: 0;left: 0;}

.sgin{background-color: rgba(0,0,0,0.3);width: 120rpx;line-height: 40rpx;border-top-left-radius: 20rpx;border-bottom-right-radius: 20rpx;text-align: center;position: absolute;top: 0;left: 0;z-index: 2;}
.hotImg{width: 260rpx;height: 300rpx;border-radius: 10rpx;}
.hotTit{width: 260rpx;}
.newImg{width: 500rpx;height: 300rpx;border-radius: 10rpx;}
.newTit{width: 500rpx;}
.yueImg{width: 690rpx;height: 416rpx;border-radius: 10rpx;}
.yueTit{width: 690rpx;}
</style>
