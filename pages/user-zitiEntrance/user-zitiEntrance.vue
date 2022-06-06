<template>
	<view>
		<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
			<view class="li" :class="current==1?'on':''" @click="change(1)">全部</view>
			<view class="li" :class="current==2?'on':''" @click="change(2)">待提货</view>
			<view class="li" :class="current==3?'on':''" @click="change(3)">已提货</view>
		</view>
		
		<view class="color2 font-24 mx-3 bg-white radius10 mb-2 shadow" v-for="(item,index) in mainData" :key="index">
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">

				<view class="color6">订单编号:{{item.order_no}}</view>
				<view class="Mcolor" v-if="item.transport_status==0">待提货</view>
				<view class="Mcolor" v-if="item.transport_status==2">已提货</view>
			</view>
			<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-writeOffOrders/user-writeOffOrders?id='+$event.currentTarget.dataset.id}})">
				<view class="d-flex a-center">
					<image v-for="(c_item,c_index) in item.child" :key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''" class="orderImg"></image>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="color9">{{item.create_time}}</view>
				<view>共{{item.child.length}}件商品 合计：￥{{item.price}}</view>
			</view>
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="d-flex a-center">订单类型：<text class="red">{{item.type==2?'包月':'普通'}}</text></view>
				<view>{{item.name?item.name:''}} {{item.phone?item.phone:''}}</view>
			</view>
		</view>
		
		<image src="../../static/images/scanl-icon.png" class="sys" 
		@click="scanCode"></image>
		
		
		<view style="height: 120rpx;"></view>
		<view class="py-3 bT-f5 p-f bottom-0 left-0 right-0 text-center bg-white dis" @click="loginOff">退出登录</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				keywords:'',
				mainData:[],
				current:1,
				searchItem:{
					user_type:0,
					thirdapp_id:2,
					pay_status:1,
					level:1,
					transport_type:2
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.searchItem.shop_no = uni.getStorageSync('staffInfo').user_no;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			self.getMainData(true)
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			loginOff(){
				const self = this;
				uni.removeStorageSync('staffInfo');
				uni.removeStorageSync('staffToken');
				self.Router.redirectTo({route:{path:'/pages/user/user'}})
			},
			
			scanCode(){
				const self = this;
				uni.scanCode({
				    success: function (res) {
				        self.getOrderData(res.result)
				    }
				});
			},
			
			getOrderData(id) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					id:id,
					user_type:0,
					shop_no:uni.getStorageSync('staffInfo').user_no
				};
				
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.Router.navigateTo({route:{path:'/pages/user-writeOffOrders/user-writeOffOrders?id='+res.info.data[0].id}})
					}else{
						self.$Utils.showToast('二维码无效')
					}
				};
				self.$apis.orderGet(postData, callback);
			},
			
			change(current) {
				const self = this;
				if(current!=self.current){
					self.current = current;
					if(self.current==1){
						delete self.searchItem.transport_status
					}else if(self.current==2){
						self.searchItem.transport_status = 0
					}else if(self.current==3){
						self.searchItem.transport_status = 2
					};
					self.getMainData(true)
				}
			},
			
			
			
			
			getMainData(isNew) {
				const self = this;
				console.log(2323)
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
						for (var i = 0; i < self.mainData.length; i++) {
							self.mainData[i].totalCount = 0;
							for (var j = 0; j < self.mainData[i].child.length; j++) {
								self.mainData[i].totalCount += self.mainData[i].child[j].count
							}
						}
					}
					//self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	};
</script>

<style>
.li{width: 33.33%;}
.orderImg{width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.tkBtn{width: 140rpx;line-height: 54rpx;text-align: center;}
.dis{height: 100rpx;}

.sys{width: 100rpx;height: 100rpx;position: fixed;top: 45%;right: 0;}
</style>
