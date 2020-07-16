<template>
	<view>
		
		<view class="vipHead pt-3 px-3 p-r bg-black">
			<view class="lq font-26 radiusR-1" @click="yesShow">领取会员</view>
			<!-- 非会员 -->
			<!-- <view class="p-r noVip">
				<image src="../../static/images/vip-icon7.png" ></image>
				<view class="p-aXY py-3 px-4 color2 font-24 line-h w-70">
					<view class="pb-5"><text class="font-40 font-w">会员VIP</text> 专享会员权益</view>
					<view>领取会员享受更多优惠</view>
				</view>
			</view> -->
			<!-- 会员 -->
			<view class="p-r yesVip">
				<image src="../../static/images/vip-icon7.png" ></image>
				<view class="p-aXY p-4 color2 font-24 line-h d-flex">
					<image src="../../static/images/vip-img.png" class="vipImg"></image>
					<view class="font-30 color2 font-w pt-1 pl-2">
						<view>帕拉欧度</view>
						<view class="font-22 color2f mt-2 d-flex colorf vipSpan">
							<image src="../../static/images/vip-icon.png" class="vipIcon2"></image>
							<view>会员</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="p-r vipBox">
			<image src="../../static/images/vip-img0.png" class="vipBg"></image>
			
			<view class="line-h color2 px-3 p-r">
				<view class="font-32 py-4 font-w">会员权益</view>
				<view class="font-26 d-flex j-sb">
					<view class="d-flex flex-column a-center">
						<image src="../../static/images/vip-icon1.png" class="vipIcon"></image>
						<view class="pt-3">专享充值</view>
					</view>
					<view class="d-flex flex-column a-center">
						<image src="../../static/images/vip-icon2.png" class="vipIcon"></image>
						<view class="pt-3">领取优惠券</view>
					</view>
					<view class="d-flex flex-column a-center">
						<image src="../../static/images/vip-icon3.png" class="vipIcon"></image>
						<view class="pt-3">专享服务</view>
					</view>
					<view class="d-flex flex-column a-center">
						<image src="../../static/images/vip-icon4.png" class="vipIcon"></image>
						<view class="pt-3">专享福利</view>
					</view>
				</view>
				
				<!-- 会员展示 -->
				<view class="pt-3">
					<view class="font-32 py-4 font-w">优惠券专区</view>
					<view class="d-flex flex-wrap j-sb">
						<view class="p-r">
							<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
							<view class="p-a colorR top-0 left-0 right-0 text-center">
								<view class="vipPrice pt-4 pb-1">10</view>
								<view class="font-18">满199元使用</view>
								<view class="font-w pt-5 font-24">立即领券</view>
							</view>
						</view>
						<view class="p-r">
							<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
							<view class="p-a colorR top-0 left-0 right-0 text-center">
								<view class="vipPrice pt-4 pb-1">10</view>
								<view class="font-18">满199元使用</view>
								<view class="font-w pt-5 font-24">立即领券</view>
							</view>
						</view>
						<view class="p-r">
							<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
							<view class="p-a colorR top-0 left-0 right-0 text-center">
								<view class="vipPrice pt-4 pb-1">10</view>
								<view class="font-18">满199元使用</view>
								<view class="font-w pt-5 font-24">立即领券</view>
							</view>
						</view>
					</view>
				</view>
				
			</view>
			
				
			
			<view class="btn690 p-a" @click="Router.redirectTo({route:{path:'/pages/VIP-recharge/VIP-recharge'}})">充值</view>
		</view>
		
		
		<view class="lq-exec p-fXY m-a radius10 text-center" v-show="yes_show">
			<view class="font-32 colorf">领取成功</view>
			<image src="../../static/images/vip-icon8.png" class="x-icon" @click="yesShow"></image>
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
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/VIP/VIP'}})">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
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
				yes_show:false
			}
		},
		methods: {
			yesShow(){
				const self = this;
				self.yes_show = !self.yes_show
				console.log(222)
			}
		}
	}
</script>

<style scoped>
page{background: #fff;}
.vipHead .noVip{width: 630rpx;height: 180rpx;}
.lq{background: #FDDFD2;width: 100rpx;height: 160rpx;position: absolute;bottom: 0;right: 30rpx;writing-mode: vertical-rl;line-height: 70rpx;color: #9C7032;padding-top: 30rpx;}
.yesVip{width: 690rpx;height: 180rpx;}
.vipImg{width: 90rpx;height: 90rpx;}
.vipIcon2{width: 32rpx;height: 32rpx;}
.vipSpan{line-height: 32rpx;background-color: #DEB883;border-radius: 16rpx;}
.vipSpan view{background-color: #DEB883;border-radius: 16rpx;text-indent: 10rpx;padding-right: 10rpx;}


.vipBox{height: 993rpx;}
.vipBg{width: 750rpx;height: 993rpx;position: absolute;top: -30rpx;}
.vipIcon{width: 90rpx;height: 90rpx;}
.btn690{bottom: 150rpx;}


.lq-exec{width: 400rpx;height: 160rpx;line-height: 160rpx;background-color: rgba(0,0,0,0.5);z-index: 100;}
.x-icon{position: absolute;right: 0;top: 0;margin: 20rpx;}
</style>
