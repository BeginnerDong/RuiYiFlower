<template>
	<view>
		
		<view class="bg-white mx-3 px-2 my-2">
			<view class="py-3 d-flex a-center j-sb" v-for="(item,index) in mainData.child" :key="index">
				<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
				item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''" class="shopImg"></image>
				<view class="shopCon d-flex flex-column">
					<view class="tit avoidOverflow pb-2">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product
							&&item.orderItem[0].snap_product?item.orderItem[0].snap_product.title:''}}</view>
					<!-- <view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view> -->
					<view class="flex1">
						<view class="price">{{item.price?item.price:''}}</view>
						<view class="font-26 color6">x{{item.price?item.count:''}}</view>
					</view>
				</view>
			</view>
		</view>
		
		<textarea  v-model="passage1"  placeholder="请写出退款原因" />
		
		<view class="btn690" v-if="mainData.transport_status==0" @click="$Utils.stopMultiClick(orderUpdate)">确定</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				mainData:{},
				passage1:''
			}
		},
		
		onLoad(options) {
			const self = this;
			uni.showLoading();
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			orderUpdate() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.passage1==''){
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请描述退款原因', 'none');
					return
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					order_step:1,
					passage1:self.passage1
				};
				postData.searchItem = {
					id:self.id,
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },
			
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {
					searchItem:{
						id:self.id,
						user_type:0
					}
				};
				postData.tokenFuncName = 'getProjectToken'
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.mainData = res.info.data[0];
					} else {
						self.$Utils.showToast(res.msg, 'none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	};
</script>

<style>
.shopCon .tit{width: 455rpx;}
textarea{width: 690rpx;height: 400rpx;background: #fff;padding: 30rpx 20rpx;box-sizing: border-box;font-size: 26rpx;margin: 0 30rpx 80rpx;border-radius: 10rpx;}
</style>
