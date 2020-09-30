<template>
	<view class="color2 font-32">
		<view class="mb-2 bg-white px-3 pb-3" v-for="(item,index) in mainData" :key="index">
			<view class="d-flex j-sb font-w py-3" @click="choose(index)">
				<view><text class="colorR">{{item.price}}</text>元套餐</view>
				<image  :src="chooseIndex==index?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'" class="shop-icon"></image>
			</view>
			<view class="d-flex j-sb font-24 text-center">
				<view class="rech borderM radius10" v-if="item.coupon.length>0">
					<view class="rechTop p-r p-1">
						<image src="../../static/images/vip-icon6.png" class="rechImg"></image>
						<view class="p-aXY colorf line-h">
							<view class="rechPrice py-2">{{item.coupon&&item.coupon[0]?item.coupon[0].value:''}}</view>
							<view>满{{item.coupon&&item.coupon[0]?item.coupon[0].condition:''}}可用</view>
						</view>
					</view>
					<view class="py-2">优惠券x{{item.behavior}}</view>
				</view>
				<view class="rech borderM radius10" v-if="item.sku1.length>0">
					<view class="rechTop p-r p-1">
						<image :src="item.sku1&&item.sku1[0]&&item.sku1[0].product&&item.sku1[0].product.mainImg&&item.sku1[0].product.mainImg[0]?item.sku1[0].product.mainImg[0].url:''" class="rechImg"></image>
					</view>
					<view class="py-2">{{item.sku1&&item.sku1[0]&&item.sku1[0].product?item.sku1&&item.sku1[0]&&item.sku1[0].product.title+item.sku1[0].title:''}}</view>
				</view>
				<view class="rech borderM radius10" v-if="item.sku2.length>0">
					<view class="rechTop p-r p-1">
						<image :src="item.sku2&&item.sku2[0]&&item.sku2[0].product&&item.sku2[0].product.mainImg&&item.sku2[0].product.mainImg[0]?item.sku2[0].product.mainImg[0].url:''" class="rechImg"></image>
					</view>
					<view class="py-2">{{item.sku2&&item.sku2[0]&&item.sku2[0].product?item.sku2&&item.sku2[0]&&item.sku2[0].product.title+item.sku2[0].title:''}}</view>
				</view>
			</view>
		</view>
		
		
		
		
		<view style="height: 180rpx;"></view>
		<view class="bg-white py-4 p-f bottom-0 left-0 right-0">
			<view class="btn690" @click="submit">立即支付</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				chooseIndex:0,
				addressData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			if(uni.getStorageSync('choosedAddressData')){
				self.addressData = uni.getStorageSync('choosedAddressData')
			}
		},
		
		methods: {
			
			choose(index){
				const self = this;
				self.chooseIndex = index
			},
			
			
			submit(){
				const self = this;
				uni.setStorageSync('canClick', false);
				if(JSON.stringify(self.addressData)=='{}'){
					uni.showModal({
						title:'提示',
						content:'请选择收货地址，用于赠送商品发货',
						
						success(res) {
							if(res.confirm){
								self.$Router.navigateTo({route:{path:'/pages/user-address/user-address'}})
							}
						}
					})
					return
				};
				var orderList = []
				/* for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({product_id:self.mainData[i].product_id,count:self.mainData[i].count,type:self.mainData[i].type})
				} */
				var data = {};
				
				orderList.push({product_id:self.mainData[self.chooseIndex].id,count:1,snap_address: self.addressData})
				
				self.addOrder(orderList)
			},
			
			addOrder(orderList) {
				const self = this;	
				
				/* if(self.orderId){
					self.goPay()
					return
				}; */
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.data = {
					level:1,
					price:self.mainData[self.chooseIndex].price,
					transport_type:1,
					snap_address:self.addressData
				};
				postData.type = 3;
				postData.parent = 1;
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = {
					wxPay:{
						price:self.mainData[self.chooseIndex].price
					}
				};	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [];
				postData.payAfter.push({
					tableName: 'FlowLog',
					FuncName: 'add',
					data: {
						type:2,
						count :100,
						trade_info:'充值',
						account:1,
						withdraw:0,
						thirdapp_id:2,
						user_no:uni.getStorageSync('user_info').user_no
					},
				});
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '充值成功',
										duration: 1000,
										success: function() {
											
										}
									});
									setTimeout(function() {
										uni.navigateBack({
											delta:1
										})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									uni.showToast({
										title: '支付失败',
										duration: 2000
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '充值成功',
								duration: 1000,
								success: function() {
									
								}
							});
							setTimeout(function() {
								uni.navigateBack({
									delta:1
								})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
				};
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:3
				};
				postData.getAfter = {
					coupon:{
						tableName:'Coupon',
						middleKey:'passage1',
						key:'coupon_no',
						searchItem:{
							status:1,
						},
						condition:'='
					},
					sku1:{
						tableName:'Sku',
						middleKey:'passage2',
						key:'sku_no',
						searchItem:{
							status:1,
						},
						condition:'='
					},
					sku2:{
						tableName:'Sku',
						middleKey:'passage3',
						key:'sku_no',
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
				self.$apis.productGet(postData, callback);
			},	
			
		}
	}
</script>

<style scoped>
.rechTop{width: 208rpx;height: 150rpx;background-color: #FDF7F5;box-sizing: border-box;}
.rechImg{width: 190rpx;height: 130rpx;}
.rechPrice{font-size: 40rpx;font-family: 'Impact';}
.rechPrice::before{content: '￥';font-size: 16rpx;font-weight: 800;}
</style>
