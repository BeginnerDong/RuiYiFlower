<template>
	<view class="line-h">
		<view class="font-50 head">账号登录</view>
		
		<view class="login font-26 pb-1">
			<input type="text" value="" placeholder="请输入手机号" />
			<input type="text" value="" placeholder="请输入密码" />
		</view>
		
		<view class="Btn600">确定</view>
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
page{background-color: #fff!important;}
.head{padding: 100rpx 0 120rpx 76rpx;}

.login input{padding: 40rpx 0 30rpx;border-bottom: 1px solid #f5f5f5;width: 600rpx;margin: auto;}
.login input::-webkit-input-placeholder{color: #999;}

.Btn600{background-color: #FF6740;width: 600rpx;height: 80rpx;line-height: 80rpx;color: #fff;font-size: 30rpx;text-align: center;border-radius: 40rpx;margin:  50rpx auto;}
</style>
