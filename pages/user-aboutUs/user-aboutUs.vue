<template>
	<view>
		
		<view class="px-3 bg-white color6 font-26">
			<button class="flex1 bB-f5 py-4" open-type="contact" style="text-align: left;background-color: #fff;">
				<image src="../../static/images/contact-usl-icon.png" class="con-icon"></image>
				<view class="font-28 color2 flex-1">在线客服</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</button>
			<view class="flex1 bB-f5 py-4">
				<image src="../../static/images/contact-usl-icon1.png" class="con-icon"></image>
				<view class="font-28 color2 flex-1">客服微信</view>
				<view>{{articleData.title}}</view>
			</view>
			<view class="flex1 bB-f5 py-4">
				<image src="../../static/images/contact-usl-icon2.png" class="con-icon"></image>
				<view class="font-28 color2 flex-1">联系电话</view>
				<view>{{articleData.small_title}}</view>
			</view>
			<view class="d-flex a-start j-sb py-4">
				<image src="../../static/images/contact-usl-icon3.png" class="con-icon"></image>
				<view class="font-28 color2 flex-1 addname">公司地址</view>
				<view class="addTxt text-right">{{articleData.description}}</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				articleData:{},
				searchItem:{
					thirdapp_id:2
				}
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.articleData = res.info.data[0]
					};
					uni.setStorageSync('canClick', true);
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
		}
	}
</script>

<style>
.con-icon{width: 50rpx;height: 50rpx;margin-right: 20rpx;}
.addname{padding-top: 5rpx;}
.addTxt{width: 360rpx;}
</style>
