<template>
	<view>
		
		<view class="font-28 color2 d-flex shadow list">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">未使用</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">已使用</view>
		</view>
		
		<view class="pt-3 px-3 line-h">
			<view class="d-flex flex-wrap j-sb">
				<view class="p-r mt-2">
					<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
					<view class="p-a colorR top-0 left-0 right-0 text-center">
						<view class="vipPrice pt-4 pb-1">10</view>
						<view class="font-18">满199元使用</view>
						<view class="font-w pt-5 font-24">立即领券</view>
					</view>
				</view>
				<view class="p-r mt-2">
					<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
					<view class="p-a colorR top-0 left-0 right-0 text-center">
						<view class="vipPrice pt-4 pb-1">10</view>
						<view class="font-18">满199元使用</view>
						<view class="font-w pt-5 font-24">立即领券</view>
					</view>
				</view>
				<view class="p-r mt-2">
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
</template>

<script>
	export default {
		data() {
			return {
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
page{background-color: #fff;}
.li{width: 50%;}
</style>
