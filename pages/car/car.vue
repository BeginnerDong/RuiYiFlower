<template>
	<view class="font-28 color2">
		<view class="d-flex j-sb p-3 bg-white bB-f5">
			<view>全部商品({{mainData.length?mainData.length:'0'}})</view>
			<view  v-show="!is_allDelt" @click="allDeltShow">管理</view>
			<view  v-show="is_allDelt" @click="allDeltShow">完成</view>
		</view>
		
		<view class="p-3 bg-white d-flex a-center j-sb mb-2"  v-for="(item,index) in mainData" :key="index">
			<image  :src="item.isSelect?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'" @click="choose(index)" class="shop-icon"></image>
			<view style="position: relative;">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="shopImg"></image>
				<!-- <view style="position: absolute;bottom: 0;width: 100%;text-align: center;background-color: #000000;opacity: 0.5;color: #fff;">
					{{item.transport_type&&item.transport_type==1?'送货上门':'自提'}}
				</view> -->
			</view>
			
			<view class="shopCon d-flex flex-column j-sb a-center">
				<view class="tit avoidOverflow pb-2">{{item.title}}</view>
				 <view class="d-flex"><view class="font-24 carSpan color6 px-1">{{item.sku&&item.sku[item.skuIndex]?item.sku[item.skuIndex].title:''}}</view></view>
				<view class="d-flex w-100 j-sb pt-2">
					<view class="price">{{item.sku&&item.sku[item.skuIndex]?item.sku[item.skuIndex].price:''}}</view>
					<view class="b-e1 d-flex a-center" style="height: 50rpx;">
						<view class="flex0 px-1 h-100" @click="counter(index,'-')">
							<image src="../../static/images/shopping-icon2.png" class="count-icon1"></image>
						</view>
						
						<input class="num bL-e1 bR-e1 text-center" v-if="countIndex==index" type="number" 
						v-model="count" @blur="blur(index)" :focus="focus" @input="change(index)">
						<view class="num bL-e1 bR-e1 text-center" v-else @click="changeCount(item,index)">{{item.count}}</view>
						
						<view class="flex0 px-1 h-100" @click="counter(index,'+')">
							<image src="../../static/images/shopping-icon3.png" class="count-icon2"></image>
						</view>
					</view>
				</view>
			</view>
		</view>

		
		
		
		
		
		
		<view :style="iPhoneX?'height: 170rpx;':'height: 130rpx'"></view>
		<view class="bg-white p-f left-0 right-0 d-flex " v-if="!is_allDelt" :style="iPhoneX?'bottom: 150rpx;':'bottom: 110rpx'">
			<view class="font-26 d-flex a-center j-sb px-3 flex-1">
				<view class="d-flex a-center">
					<image @click="chooseAll" class="shop-icon"
					:src="isChooseAll?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'"></image>
					<view class="pl-1">全选</view>
				</view>
				<view class="font-22 d-flex a-center">合计 <text class="price font-30">{{totalPrice}}</text></view>
			</view>
			<view class="carBtn" @click="pay">立即购买</view>
		</view>
		<view class="bg-white p-f left-0 right-0 d-flex a-center j-sb px-3 " v-else :style="iPhoneX?'bottom: 150rpx;':'bottom: 110rpx'">
			<view class="d-flex a-center">
				<image  @click="chooseAll" :src="isChooseAll?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'" class="shop-icon"></image>
				<view class="pl-1 font-26">全选</view>
			</view>
			<view class="font-23 borderM radius30 deleteBtn" @click="deleteAll()">删除</view>
		</view>
		
		
		<!-- footer -->
		<view class="footer" :class="iPhoneX?'D':''">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1.png" mode=""></image>
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
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4-a.png" mode=""></image>
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
				iPhoneX:false,
				showView: false,
				wx_info:{},
				is_show:false,
				count:1,
				mainData:[],
				is_allDelt:false,
				totalPrice:0,
				isChooseAll:true,
				
				count:0,
				countIndex:-1,
				focus:false,
			}
		},
		
		onLoad() {
			const self = this;
			if (uni.getStorageSync('isIphoneX')) {
				self.iPhoneX = true;
			}
			// self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			self.mainData = self.$Utils.getStorageArray('cartData');
			console.log('self.mainData',self.mainData)
			self.checkChooseAll();
			self.countTotalPrice();
		},
		
		methods: {
			
			changeCount(item,index){
				const self = this;
				self.count = item.count;
				self.countIndex = index;
				self.focus = true;
			},
			
			change(index){
				const self = this;
				if(parseInt(self.count)<=0){
					uni.showToast({
						title:'输入数量有误',
						duration:1500,
						icon:'none'
					})
					self.mainData[index]['count'] = 1;
				}else{
					self.mainData[index]['count'] = parseInt(self.count); 
				}
				self.$Utils.setStorageArray('cartData', self.mainData[index], 'id', 999);
				self.countTotalPrice();
				console.log(self.count,self.countIndex)
			},
			
			blur(index){
				const self = this;
				if(!self.count){
					uni.showToast({
						title:'输入数量有误',
						duration:1500,
						icon:'none'
					})
					self.mainData[index]['count'] = 1;
				}
				self.countTotalPrice();
				self.count = 0;
				self.countIndex = -1;
				self.focus = false;
				console.log(self.count,self.countIndex)
			},
			
			pay(e) {
				const self = this;
				const orderList = [
				];
				for (var i = 0; i < self.mainData.length; i++) {
					if (self.mainData[i].isSelect) {
						orderList.push(
							{sku_id:self.mainData[i].sku[self.mainData[i].skuIndex].id,count:self.mainData[i].count,
							product:self.mainData[i],skuIndex:self.mainData[i].skuIndex,transport_type:self.mainData[i].transport_type?self.mainData[i].transport_type:0},
						);
					};
				};
				if (orderList.length == 0) {
					self.$Utils.showToast('未选择商品', 'none', 1000);
					return;
				};
				// for (var i = 0; i < orderList.length; i++) {
				// 	if(i<orderList.length-1){
				// 		if(orderList[i].transport_type!=orderList[i+1].transport_type){
				// 			self.$Utils.showToast('所选商品收货方式不同，不能同时下单', 'none', 1000);
				// 			return;
				// 		}
				// 	}				
				// };
				uni.setStorageSync('payPro', orderList);
				self.$Router.navigateTo({
					route: {
						path: '/pages/car-order/car-order?type='+orderList[0].transport_type
					}
				})
			},
			
			checkChooseAll() {
				const self = this;
				var isChooseAll = true;
				for (var i = 0; i < self.mainData.length; i++) {
					if (!self.mainData[i].isSelect) {
						isChooseAll = false;
					};
				};
				self.isChooseAll = isChooseAll;
			},
			
			chooseAll() {
				const self = this;
				self.isChooseAll = !self.isChooseAll;
				for (var i = 0; i < self.mainData.length; i++) {
					self.mainData[i].isSelect = self.isChooseAll;
					self.$Utils.setStorageArray('cartData', self.mainData[i], 'id', 999);
				};
				self.countTotalPrice();
			},
			
			allDeltShow(){
				const self = this;
				self.is_allDelt = !self.is_allDelt
			},
			
			blur(){
				const self = this;
				
			},
			
			counter(index,type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.$Utils.setStorageArray('cartData', self.mainData[index], 'id', 999);
				self.countTotalPrice();
			},
			
			deleteAll() {
				const self = this;
				uni.showModal({
					title: '提示',
					content: '确认要删除选中商品吗？',
					showCancel: true,
					cancelText: '取消',
					confirmText: '确认',
					success: res => {
						if (res.confirm) {
							for (var i = 0; i < self.mainData.length; i++) {
								if(self.mainData[i].isSelect){
									self.$Utils.delStorageArray('cartData', self.mainData[i], 'id');
								}
							};
							self.mainData = self.$Utils.getStorageArray('cartData');
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					},
				});
			},
			
			
			
			choose(index) {
				const self = this;
				
				if (self.mainData[index].isSelect) {
					self.mainData[index].isSelect = false;
				} else {
					self.mainData[index].isSelect = true;
				};
				self.$Utils.setStorageArray('cartData', self.mainData[index], 'id', 999);
				
				self.checkChooseAll();
				self.countTotalPrice();
			},
			
			countTotalPrice() {
				const self = this;
				self.totalPrice = 0;
				
				for (var i = 0; i < self.mainData.length; i++) {
					if (self.mainData[i].isSelect) {
						var count = self.mainData[i].count?self.mainData[i].count:0
						self.totalPrice += self.mainData[i].sku[self.mainData[i].skuIndex].price * count;
					};
				};
				self.totalPrice = self.totalPrice.toFixed(2)
				console.log(self.totalPrice)
			},
			
			
			
		}
	};
</script>


<style scoped>
.shopImg{width: 183rpx;height: 183rpx;}
.shopCon{width: 438rpx;height: 183rpx;}
.shopCon .tit{width: 438rpx;}
.carSpan{background-color: #FDF7F5;line-height: 36rpx;}

.deleteBtn{width: 160rpx;line-height: 60rpx;text-align: center;color: #FF6740;height: 60rpx;}
.carBot{bottom: 110rpx;}

.num{width: 80rpx;}
</style>
