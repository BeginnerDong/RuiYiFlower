<template>
	<view>
		
		<view class="color2 font-24 m-2 bg-white radius10">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：22222</view>
					<view class="color9">2020-06-23 15:30:25</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" >
					<image src="../../static/images/home-icon4.png" class="orderImg"></image>
					<view class="flex-1 pl-3 py-1 d-flex flex-column j-sb txt">
						<view>名称名称</view>
						<view class="price font-32">200</view>
					</view>
				</view>
				<view class="py-3 px-2">
					<textarea value="" placeholder="请输入您想说的话" />
					
					<view class="pb-2">添加图片（1/4）</view>
					<view class="flex">
						<image src="../../static/images/icon5.png" class="wh120"></image>
					</view>
					
					<view class="btn690">提交</view>
				</view>
			</view>
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

<style scoped>
	textarea{display: block;width: 100%;}
.wh120{width: 120rpx;height: 120rpx;margin-right: 20rpx;}
.btn690{width: 100%;margin: 220rpx 0 20rpx;}
.orderImg {width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.txt{height: 125rpx;}
</style>
