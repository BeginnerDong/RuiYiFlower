<template>
	<view class="h-100">
		
		<view class="h-100 d-flex">
			<view class="left line-h h-100 font-26 color6">
				<view class="py-3 classLi" @click="changeLeft(0)" :class="leftCurr==0?'on':''">为您推荐</view>
				<view class="py-3 classLi" @click="changeLeft(1)" :class="leftCurr==1?'on':''">包月鲜花</view>
				<view class="py-3 classLi" @click="changeLeft(2)" :class="leftCurr==2?'on':''">礼品花束</view>
				<view class="py-3 classLi" @click="changeLeft(3)" :class="leftCurr==3?'on':''">绿植多肉</view>
				<view class="py-3 classLi" @click="changeLeft(4)" :class="leftCurr==4?'on':''">应季鲜花</view>
				<view class="py-3 classLi" @click="changeLeft(5)" :class="leftCurr==5?'on':''">盆栽绿植</view>
				<view class="py-3 classLi" @click="changeLeft(6)" :class="leftCurr==6?'on':''">鲜花周边</view>
				<view class="py-3 classLi" @click="changeLeft(7)" :class="leftCurr==7?'on':''">开业花篮</view>
				<view class="py-3 classLi" @click="changeLeft(8)" :class="leftCurr==8?'on':''">进口鲜花</view>
			</view>
			
			<view class="right h-100 bg-white flexY flex-column flex-1">
				<view class="p-3 pb-1 d-flex" @click="Router.redirectTo({route:{path:'/pages/goodsDetail/goodsDetail'}})">
					<image src="../../static/images/classificationl-img.png" class=""></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">郁金香 11枝粉色+黄色</view>
						<view class="d-flex j-sb">
							<view class="price font-28">36.0</view>
							<view class="font-22 color9">销量:255</view>
						</view>
					</view>
				</view>
				<view class="p-3 pb-1 d-flex">
					<image src="../../static/images/classificationl-img.png" class=""></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">郁金香 11枝粉色+黄色</view>
						<view class="d-flex j-sb">
							<view class="price font-28">36.0</view>
							<view class="font-22 color9">销量:255</view>
						</view>
					</view>
				</view>
				<view class="p-3 pb-1 d-flex">
					<image src="../../static/images/classificationl-img.png" class=""></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">郁金香 11枝粉色+黄色</view>
						<view class="d-flex j-sb">
							<view class="price font-28">36.0</view>
							<view class="font-22 color9">销量:255</view>
						</view>
					</view>
				</view>
				<view class="p-3 pb-1 d-flex">
					<image src="../../static/images/classificationl-img.png" class=""></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">郁金香 11枝粉色+黄色</view>
						<view class="d-flex j-sb">
							<view class="price font-28">36.0</view>
							<view class="font-22 color9">销量:255</view>
						</view>
					</view>
				</view>
				<view class="p-3 pb-1 d-flex">
					<image src="../../static/images/classificationl-img.png" class=""></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">郁金香 11枝粉色+黄色</view>
						<view class="d-flex j-sb">
							<view class="price font-28">36.0</view>
							<view class="font-22 color9">销量:255</view>
						</view>
					</view>
				</view>
			</view>
			
		</view>
		
		
		
		
		
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
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
				leftCurr:0
			}
		},
		methods: {
			changeLeft(i){
				const self = this;
				self.leftCurr = i
			}
		}
	}
</script>

<style>
page{height: 100%;}

.left{width: 180rpx;padding-bottom: 100rpx;}
.left .classLi{text-align: center;margin-bottom: 40rpx;}
.left .on{color: #FF6740;position: relative;}
.left .on::before{content: ''; height: 60rpx;width: 14rpx;border-radius: 7rpx;background-color: #FF6740;position: absolute;left: -7rpx;top: 14rpx;}

.right{padding-bottom: 120rpx;}
.right image{width: 200rpx;height: 140rpx;}
.right .tt{width: 320rpx;}
</style>
