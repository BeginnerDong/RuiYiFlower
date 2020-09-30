<template>
	<view>
		
		<view class="font-32 color2 font-w pt-3 px-3">优惠券专区</view>
		<view class="pt-3 px-3 line-h">
			<view class="d-flex flex-wrap coupons">
				<view class="p-r mt-3" v-for="(item,index) in mainData" :key="index">
					<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
					<view class="p-a colorR top-0 left-0 right-0 text-center">
						<view class="vipPrice pt-4 pb-1">{{item.value}}</view>
						<view class="font-18">满{{item.condition}}元使用</view>
						<view class="font-w pt-5 font-24" @click="submit(index)" v-if="item.hasPick&&item.hasPick.length==0">立即领券</view>
						<view class="font-w pt-5 font-24" v-else>已领取</view>
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
				mainData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			const callback = (res) => {
				self.$Utils.loadAll(['getMainData'], self);
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			})
			
		},
		
		methods: {
				
			submit(index){
				const self = this;
				self.orderList = [
					{coupon_id:self.mainData[index].id,count:1,type:self.mainData[index].type}
				];
				self.couponAdd()
			},
			
			couponAdd() {
				const self = this;
				var now =  (new Date()).getTime();
				const postData = {
					
					tokenFuncName: 'getProjectToken',
					
				};
				postData.couponList = self.$Utils.cloneForm(self.orderList);
				postData.pay = {
					score: 0
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res && res.solely_code == 100000) {
						self.$Utils.showToast('领取成功', 'none')
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						self.$Utils.showToast(res.msg, 'none')
					}
				};
				self.$apis.couponAdd(postData, callback);
			},
				
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
				};
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					on_shelf:1
				};
				postData.getAfter = {
					hasPick:{
						token:uni.getStorageSync('user_token'),
						tableName:'UserCoupon',
						middleKey:'coupon_no',
						key:'coupon_no',
						searchItem:{
							status:1,
						},
						condition:'='
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.couponGet(postData, callback);
			},	
				
		}
	}
</script>

<style>
page{background-color: #fff;}
.coupons>view{margin-right: 26rpx;}
.coupons>view:nth-child(3n){margin-right: 0;}
</style>
