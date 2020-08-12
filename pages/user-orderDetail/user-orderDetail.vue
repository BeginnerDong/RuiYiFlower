<template>
	<view>
		<view class="bg-white py-3 px-2 mx-3 mt-2 radius10 overflow-h line-h d-flex a-center j-sb p-r mb-2">
			<!-- 核销显示 -->
			<view class="font-26" v-if="mainData.transport_type==2">
				<view class="pb-3">收货人：{{mainData.name?mainData.name:''}} {{mainData.phone?mainData.phone:''}}</view>
				<view class="colorR pb-3">{{mainData.shop&&mainData.shop.name?mainData.shop.name:''}}</view>
				<view class="color6 pb-3">地址：{{mainData.shop&&mainData.shop.address?mainData.shop.address:''}}</view>
				<view class="color6">电话：{{mainData.shop&&mainData.shop.phone?mainData.shop.phone:''}}</view>
			</view>
			<!-- 包月、快递订单显示 -->
			<view class="font-26" v-if="mainData.transport_type==1">
				<view class="pb-3">{{mainData.snap_address&&mainData.snap_address.name?mainData.snap_address.name:''}}
					{{mainData.snap_address&&mainData.snap_address.phone?mainData.snap_address.phone:''}}</view>
				<view>{{mainData.snap_address.city+mainData.snap_address.detail}}</view>
			</view>


			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a top-0 left-0 right-0"></image>
		</view>

		<view class="bg-white mx-3 px-2 mt-2">
			<view class="py-3 d-flex a-center j-sb" v-for="(item,index) in mainData.child" :key="index"
			@click="Router.navigateTo({route:{path:'/pages/user-orderComment/user-orderComment'}})">
				<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
								item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''"
				 class="shopImg"></image>
				<view class="shopCon d-flex flex-column">
					<view class="tit avoidOverflow pb-2">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product?item.orderItem[0].snap_product.title:''}}</view>
					<!-- <view class="d-flex">
						<view class="font-24 carSpan mb-5 color6 px-1">精品大束</view>
					</view> -->
					<view class="flex1">
						<view class="price">{{item.unit_price}}</view>
						<view class="font-26 color6">x{{item.count}}</view>
					</view>
				</view>
			</view>
			<!-- 自提订单显示 -->
			<view class="d-flex a-center j-sb py-3 bT-f5" @click="hxEwmShow()" v-if="mainData.transport_type==2">
				<view>提货码：</view>
				<image :src="mainData.qrcode" class="hx-icon"></image>
			</view>
		</view>
		
		<view class="bg-white mx-3 radius10 mt-2 font-24 color9 px-2 pb-3" v-if="mainData.type==2">
			<view class="flex1 py-3 bB-f5 color2 mb-3">
				<view>包月详情</view>
			</view>
			<view class="flex1 pb-3"  v-for="(item,index) in mainData.log" :key="index">
				<view class="">第{{index+1}}次收花时间：{{Utils.timeto(parseInt(item.passage)*1000,'ymd')}}</view>
				<view><text class="red font-28">{{item.behavior==1?'已收':'未收'}}</text></view>
			</view>
			
		</view>

		<view class="bg-white mx-3 radius10 mt-2 font-24 color9 px-2 pb-3">
			<view class="flex1 py-3 bB-f5 color2 mb-3">
				<view>共{{mainData.child?mainData.child.length:''}}件商品</view>
				<view>合计：<text class="price font-28">{{mainData.price}}</text></view>
			</view>
			<view class="d-flex j-end pb-2">
				<view class="tkBtn b-e1 radius10">申请退款</view>
			</view>
			<!-- <view class="pb-3">支付方式：<text class="colorR">线下支付</text></view> --><!-- 包月订单显示 -->
			<view class="pb-3">订单编号：{{mainData.order_no}}</view>
			<view>下单时间：{{mainData.create_time}}</view>
		</view>

		<view class="bg-white mx-3 radius10 mt-2 font-28 color2 px-2 pb-3" v-if="mainData.order_step>0">
			<view class="py-3">退款原因</view>
			<view class="font-26 color6">{{mainData.passage1?mainData.passage1:''}}</view>
		</view>
		
		<view class="black-bj" v-show="is_hxEwmShow"></view>
		<view class="hxEwmShow" v-show="is_hxEwmShow">
			<view>
				<image class="ewm" :src="mainData.qrcode" mode=""></image>
			</view>
			<view class="closeBtn" @click="hxEwmShow">×</view>
		</view>
		
		<view style="height: 50rpx;"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				mainData: {},
				Utils:this.$Utils,
				is_hxEwmShow:false,
			}
		},

		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
			
		},

		methods: {
			
			hxEwmShow(index) {
				const self = this;
				self.is_show = !self.is_show
				self.is_hxEwmShow = !self.is_hxEwmShow
			},

			previewImg() {
				const self = this;
				var urls = [self.mainData.qrcode]
				uni.previewImage({
					urls: urls,
					longPressActions: {
						itemList: ['发送给朋友', '保存图片', '收藏'],
						success: function(data) {

						},
						fail: function(err) {
							console.log(err.errMsg);
						}
					}
				});
			},

			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				postData.getAfter = {
					shop: {
						tableName: 'UserInfo',
						middleKey: 'shop_no',
						key: 'user_no',
						searchItem: {
							status: 1,
							user_type: 1
						},
						condition: '=',
						info: ['name', 'address','phone']
					}
				};
				
				postData.getAfter.log = {
					tableName: 'Log',
					middleKey: 'id',
					key: 'relation_id',
					searchItem: {
						status: 1,
					},
					condition: '=',
				}
				
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						/* if(self.mainData.type==2){
							for (var i = 0; i < self.mainData.log.length; i++) {
								if(self.mainData.log[i].behavior==0){
									self.mainData.log[i]
								}
							}
						} */
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
		}
	};
</script>

<style>
	.shopCon .tit {
		width: 455rpx;
	}
	.hxEwm {
		width: 80rpx;
		height: 80rpx;
	}
	
	.tkBtn {
		width: 140rpx;
		line-height: 54rpx;
		text-align: center;
	}
	
	.hxEwm image {
		width: 100%;
		height: 100%;
	}
	
	.hxEwmShow {
		width: 70%;
		position: fixed;
		top: 45%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 50;
	}
	
	.hxEwmShow .ewm {
		width: 400rpx;
		height: 400rpx;
		display: block;
		margin: 0 auto;
	}
	
	.closeBtn {
		background: rgba(0, 0, 0, 0.5);
		border: 0;
		top: auto;
		bottom: -130rpx;
	}
</style>
