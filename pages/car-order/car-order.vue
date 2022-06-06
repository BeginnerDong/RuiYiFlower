<template>
	<view class="color2 font-28">
		<view class="bg-white bB-f5">
			<view class="px-3 py-2 d-flex orderList">
				<view class="orderLi borderM radiusL" :class="orderLiCurr==0?'on':''" @click="changeOrderLi(0)">到店自提
				</view>
				<view class="orderLi borderM radiusR" :class="orderLiCurr==1?'on':''" @click="changeOrderLi(1)">送货上门
				</view>
			</view>
		</view>
		<view class="bg-white line-h p-r pb-1 mb-2" v-show="orderLiCurr==0">
			<view class="p-3 line-h d-flex a-center j-sb p-r"
				@click="Router.navigateTo({route:{path:'/pages/user-store/user-store?type=0'}})">
				<view v-if="shopData.address">
					<view class="pb-3">{{shopData.name}} {{shopData.phone}}</view>
					<view>{{shopData.address}}</view>
				</view>
				<view v-else>
					<view class="">请选择自提门店</view>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
			<view class="flex1 px-3 font-24 text-center pb-2 zt">
				<input type="text" v-model="orderInfo.name" placeholder="姓名" />
				<input type="number" v-model="orderInfo.phone" maxlength="11" placeholder="电话" />
			</view>
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a bottom-0 left-0 right-0"></image>
		</view>

		<view class="bg-white line-h p-r pb-1 mb-2" v-show="orderLiCurr==1">
			<view class="p-3 line-h d-flex a-center j-sb p-r"
				@click="Router.navigateTo({route:{path:'/pages/user-address/user-address'}})">
				<view v-if="addressData.name">
					<view class="pb-3">{{addressData.name}} {{addressData.phone}}</view>
					<view>{{addressData.city+addressData.detail}}</view>
				</view>
				<view v-else>
					<view class="">选择收货地址</view>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a bottom-0 left-0 right-0"></image>
		</view>
		
		<!-- <view class="bg-white line-h p-r pb-1 mb-2" v-show="orderLiCurr==1">
			<view class="p-3 line-h d-flex a-center j-sb p-r">
				<view v-if="shopData.address">
					<view class="pb-3">{{shopData.name}} {{shopData.phone}}</view>
					<view>{{shopData.address}}</view>
				</view>
				<view v-else>
					<view class="">请选择配送门店</view>
				</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
		</view> -->

		<view class="bg-white px-3 mb-2" v-for="(item,index) in mainData" :key="index">
			<view class="py-3 d-flex a-center j-sb bB-f5">
				<image :src="item.product&&item.product.mainImg&&item.product.mainImg[0]?item.product.mainImg[0].url:''"
					class="shopImg"></image>
				<view class="shopCon d-flex flex-column flex-1 j-sb pl-2" style="height: 200rpx;">
					<view class="tit avoidOverflow pb-2">{{item.product&&item.product.title?item.product.title:''}}
					</view>
					<view class="d-flex">
						<view class="font-24 carSpan color6 px-1 d-inline-block">
							{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].title:''}}
						</view>
					</view>
					<view class="flex-1"></view>
					<view class="flex1">
						<view class="price">
							{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].price:''}}
						</view>
						<!-- <view>x{{item.count}}</view> -->
					</view>
				</view>
			</view>
			<view class="d-flex a-center j-sb py-3">
				<view>购买数量</view>
				<!-- <view class="b-e1 d-flex a-center count">
					<view class="flex0 px-1 h-100" @click="counter(index,'-')">
						<image src="../../static/images/shopping-icon2.png" class="count-icon1"></image>
					</view>
					<view class="num bL-e1 bR-e1 text-center">{{item.count}}</view>
					<view class="flex0 px-1 h-100" @click="counter(index,'+')">
						<image src="../../static/images/shopping-icon3.png" class="count-icon2"></image>
					</view>
				</view> -->
				
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

		<view class="bg-white px-3">
			<!-- <view class="py-3 bB-f5 flex1" v-show="orderLiCurr==1">
				<view>运费</view>
				<view class="font-24 color6">￥{{delivery}}</view>
			</view> -->
			<view class="py-3 flex1">
				<view>支付方式</view>
				<view class="font-24 flex0" @click="changePayType(2)" v-show="orderLiCurr==1&&firstTime==0">
					<image
						:src="payType==2?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'"
						class="shop-icon"></image>
					<view class="pl-1">货到付款</view>
				</view>
				<view class="font-24 flex0" @click="changePayType(1)">
					<image
						:src="payType==1?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'"
						class="shop-icon"></image>
					<view class="pl-1">立即支付</view>
				</view>
			</view>
			<view class="py-3 flex1" v-if="firstTime>0">
				<view>第一次收花时间</view>
				<view class="font-24" style="color:#FF6740">{{Utils.timeto(firstTime*1000,'ymd')}}</view>
			</view>

			<view class="py-3 bB-f5 flex1">
				<view>优惠券</view>
				<view class="d-flex j-end a-center color6 font-26" v-if="couponData.length==0">
					暂无优惠券使用
				</view>
				<view class="d-flex j-end a-center color6 font-26" v-if="couponData.length>0&&chooseCoupon.length==0"
					@click="couponShow">
					{{couponData.length}}张优惠券
				</view>
				<view class="d-flex j-end a-center color6 font-26" v-if="couponData.length>0&&chooseCoupon.length>0"
					@click="couponShow">
					优惠券抵扣-{{pay.coupon[0].price}}
				</view>
			</view>

			<view class="py-3 bB-f5 flex1" v-if="orderLiCurr==1">
				<view>运费</view>
				<view class="d-flex j-end a-center font-26">
					{{f_price>0&&!is_free?'￥'+f_price:'包邮'}}
				</view>
			</view>
		</view>


		<view style="height: 120rpx;width: 100%;"></view>
		<view class="bg-white p-f left-0 right-0 d-flex carBot">
			<view class="font-22 d-flex a-center flex-1 px-3">合计
				<text class="price font-30">{{totalPrice}}</text>
				<text v-if="orderLiCurr==1&&!is_free">+<text class="price font-30">{{f_price}}</text></text>
			</view>
			<button style="border-radius: 0;font-size: 15px;" class="carBtn" @click="submit">确认订单</button>
		</view>


		<!-- 充值免费领弹窗 -->
		<view class="bg-mask" v-show="free_show">
			<view class="exec p-aXY m-a bg-white radius20 font-30 color2 flex5 pb-5">
				<view class="py-5">充值免费领</view>
				<image src="../../static/images/img.png" class="lb"></image>
				<view class="btn690" @click="Router.navigateTo({route:{path:'/pages/VIP-recharge/VIP-recharge'}})">立即充值
				</view>
				<image src="../../static/images/detailsl-icon4.png" class="x-icon p-a top-0 right-0 m-3"
					@click="freeShow"></image>
			</view>
		</view>

		<view class="black-bj" v-show="is_show"></view>
		<view class="couponShow whiteBj radius10" v-show="is_couponShow">
			<view class="d-flex j-sb px-3 py-3 border-bottom">
				<view class="font-26 color9" @click="couponShow">取消</view>
				<view class="">优惠券</view>
				<view class="font-26 main-text-color" @click="useCoupon">确定</view>
			</view>


			<view class="pt-1 font-26">
				<view class="item d-flex j-sb a-center px-3 mt-3" v-for="(item,index) in couponData" :key="index"
					@click="couponChange(index)">
					<view>满{{item.condition}}减{{item.value}}元</view>
					<view class="seltIcon">
						<image
							:src="couponCurr==index?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'"
							mode=""></image>
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
				Router: this.$Router,
				orderLiCurr: 0,
				free_show: false,
				shopData: {},
				addressData: {},
				mainData: [],
				totalPrice: 0,
				orderInfo: {
					name: '',
					phone: ''
				},
				delivery: 0,
				Utils: this.$Utils,
				firstTime: 0,
				logArray: [],
				payType: 1,
				pay: {
					coupon: []
				},
				couponData: [],
				chooseCoupon: [],
				is_couponShow: false,
				is_show: false,
				couponCurr: -1,

				storeData: {},
				f_price: 0,
				allPrice: 0,
				is_free:false,
				
				count:0,
				countIndex:-1,
				focus:false,
			}
		},

		onLoad(options) {
			const self = this;
			uni.showLoading();
			//self.$Utils.loadAll(['getUserData'], self);
			if (options.type) {
				self.orderLiCurr = options.type
			};
			const callback = (res) => {
				self.$Utils.loadAll(['getUserData', 'getUserCouponData'], self);
				self.mainData = uni.getStorageSync('payPro');
				//self.countTotalPrice()
				if (options.week && options.week > 0) {
					self.week = options.week
					self.creatLog()
				};
				self.getUserInfoData()
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			})
		},

		onShow() {
			const self = this;
			if (uni.getStorageSync('choosedShopData')) {
				self.shopData = uni.getStorageSync('choosedShopData');
				console.log('shopData', self.shopData,self.totalPrice)
			}
			if (uni.getStorageSync('choosedAddressData')) {
				self.addressData = uni.getStorageSync('choosedAddressData');
				self.getStoreData();
			} else {
				self.getAddressData()
			};
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

			getStoreData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_type: 1,
					thirdapp_id: 2,
					behavior: 1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.storeData = res.info.data[0];
						self.getDistance();
					};
				};
				self.$apis.commonUserGet(postData, callback);
			},

			// 计算距离
			getDistance() {
				const self = this;
				const postData = {};
				if (!self.storeData.id || !self.addressData.id) {
					return;
				}
				postData.paths = [{
						lat: self.addressData.latitude,
						lng: self.addressData.longitude,
					},
					{
						lat: self.storeData.info.latitude,
						lng: self.storeData.info.longitude,
					}
				]
				const callback = (res) => {
					if (res.solely_code == 100000) {
						var distance = Math.ceil(res.info / 1000);
						var dis = 0; //超出起始距离数
						if (self.storeData.id) {
							if (distance > parseInt(self.storeData.info.distance)) {
								dis = distance - parseInt(self.storeData.info.distance);
							}
							console.log('distance', dis, self.is_free)
							self.f_price = parseFloat(self.storeData.info.f_price) + dis * parseFloat(self.storeData.info.a_price);
							self.f_price = parseFloat(self.f_price).toFixed(2);
						}
						console.log('f_price', self.f_price, distance)
					};
				};
				self.$apis.getShortPath(postData, callback);
			},

			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no: uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.orderInfo.name = res.info.data[0].name
						self.orderInfo.phone = res.info.data[0].phone
					}
				};
				self.$apis.userInfoGet(postData, callback);
			},

			counter(index, type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.countTotalPrice();
			},

			getUserCouponData() {
				const self = this;
				var now = Date.parse(new Date());
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					use_step: 1,
					//pay_status:1,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.couponData.push.apply(self.couponData, res.info.data)
					}
					self.$Utils.finishFunc('getUserCouponData');
				};
				self.$apis.userCouponGet(postData, callback);
			},

			useCoupon() {
				const self = this;
				self.couponTotalPrice = self.$Utils.addItemInArray(self.pay.coupon, 'price');
				/* 	console.log(index)
					console.log(self.couponData);
					console.log(self.couponData[0]); */
				/* for (var i = 0; i < self.mainData.length; i++) {
					self.totalPrice += parseFloat(parseFloat(self.mainData[i].product.sku[self.mainData[i].skuIndex].price)*parseFloat(self.mainData[i].count)).toFixed(2)
				}; */
				console.log('self.totalPrice', self.totalPrice)
				if (self.couponData[self.couponCurr] && self.couponData[self.couponCurr].id) {
					var id = self.couponData[self.couponCurr].id;
				} else {
					self.pay.coupon = []
					self.chooseCoupon = [];
					self.is_show = !self.is_show;
					self.is_couponShow = !self.is_couponShow;
					self.countTotalPrice();
					console.log('self.pay', self.pay)
					return
				}

				var findCoupon = self.$Utils.findItemInArray(self.couponData, 'id', id);
				var findItem = self.$Utils.findItemInArray(self.pay.coupon, 'id', id);
				console.log('findCoupon', findCoupon)
				self.showCoupon = false;

				if (findCoupon) {
					findCoupon = findCoupon[1];
					var findSameCoupon = self.$Utils.findItemsInArray(self.pay.coupon, 'product_id', id);
				} else {
					self.$Utils.showToast('优惠券错误', 'none');
					return;
				};
				if (findItem) {
					self.is_show = !self.is_show;
					self.is_couponShow = !self.is_couponShow;
					self.countTotalPrice();
					console.log('self.pay', self.pay)
					return
				} else {
					console.log('self.totalPrice', self.totalPrice)
					console.log('self.totalPrice', self.couponTotalPrice)
					console.log('self.totalPrice', findCoupon.condition)
					if ((self.totalPrice - self.couponTotalPrice) < findCoupon.condition) {
						self.$Utils.showToast('未达满减标准', 'none');
						return;
					};
					self.pay = {
						coupon: []
					};
					console.log('findSameCoupon.length', findSameCoupon.length)
					if (self.pay.coupon.length >= 1) {
						self.$Utils.showToast('叠加使用超限', 'none');

						return;
					};

					if (findCoupon.type == 1) {
						var couponPrice = findCoupon.value;
						console.log('findCoupon.discount', findCoupon.discount)
					} else if (findCoupon.type == 2) {

						var couponPrice = parseFloat(self.totalPrice).toFixed(2) - parseFloat(findCoupon.discount / 100 *
								self.totalPrice)
							.toFixed(2);
					};
					/* if (parseFloat(couponPrice) + parseFloat(self.couponTotalPrice) > parseFloat(self.totalPrice)) {
						couponPrice = parseFloat(self.totalPrice).toFixed(2) - parseFloat(self.couponTotalPrice).toFixed(2);
					}; */
					self.pay.coupon.push({
						id: id,
						price: couponPrice.toFixed(2),
					});
					self.chooseCoupon.push({
						id: id,
						price: couponPrice,
					});
				};
				self.is_show = !self.is_show;
				self.is_couponShow = !self.is_couponShow;
				self.countTotalPrice();
			},

			couponChange(index) {
				const self = this;
				if (self.couponCurr != index) {
					self.couponCurr = index;
				} else {
					self.couponCurr = -1
				}
			},

			couponShow() {
				const self = this;
				self.is_show = !self.is_show;
				self.is_couponShow = !self.is_couponShow;
			},

			freeShow() {
				const self = this;
				self.free_show = !self.free_show;
			},

			changePayType(type) {
				const self = this;
				self.payType = type
			},

			creatLog() {
				const self = this;
				//console.log('creatLog',self.week);
				var now = new Date();
				var today = new Date(new Date().toLocaleDateString()).getTime() / 1000;
				console.log(today)
				var day = now.getDay();
				if (day == self.week) {
					self.firstTime = today + 86400 * 7
				} else if (day > self.week) {
					var num = 7 - (parseInt(day) - parseInt(self.week));
					self.firstTime = today + 86400 * num
				} else if (day < self.week) {
					var num = parseInt(self.week) - parseInt(day);
					self.firstTime = today + 86400 * num
				};
				self.endTime = self.firstTime + 86400 * 7 * (self.mainData[0].product.sku[self.mainData[0].skuIndex]
					.score - 1)
				console.log(self.endTime)
				for (let i = 0; i < self.endTime - self.firstTime + 86400 * 7; i += 86400 * 7) {
					self.logArray.push(i + self.firstTime)
				};
				console.log('self.logArray', self.logArray)
			},

			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				if (self.orderLiCurr == 0) {
					if (JSON.stringify(self.shopData) == '{}') {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请选择自提门店', 'none', 1000)
						return;
					}
					if (self.orderInfo.name == '' || self.orderInfo.phone == '') {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请填写提货人信息', 'none')
						return
					}
					if (self.orderInfo.phone.trim().length != 11 || !/^1[3|4|5|6|7|8|9]\d{9}$/.test(self.orderInfo
							.phone)) {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请输入正确的手机号', 'none', 1000)
						return;
					}
				} else {
					if (JSON.stringify(self.addressData) == '{}') {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请选择收货地址', 'none')
						return
					}
				};
				var orderList = []
				/* for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({product_id:self.mainData[i].product_id,count:self.mainData[i].count,type:self.mainData[i].type})
				} */
				var data = {
					f_price: self.orderLiCurr == 1&&!self.is_free ? self.f_price : 0
				};
				for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({
						sku_id: self.mainData[i].sku_id,
						count: self.mainData[i].count,
						data: data,
						snap_address: self.addressData
					})
				}
				self.addOrder(orderList)
				// const callback = (user, res) => {
				// 	self.addOrder(orderList)
				// };
				// self.$Utils.getAuthSetting(callback);
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
					level: 1,
					price: self.pay.wxPay.price,
					// price: self.pay.other.price,
					f_price: self.orderLiCurr == 1&&!self.is_free ? self.f_price : 0,
					pay_type: self.payType
				};
				postData.type = 1;
				postData.parent = 1;
				postData.tokenFuncName = 'getProjectToken';
				if (self.orderLiCurr == 0) {
					postData.data.name = self.orderInfo.name
					postData.data.phone = self.orderInfo.phone
					postData.data.shop_no = self.shopData.user_no
					postData.data.transport_type = 2
				} else {
					postData.data.snap_address = self.addressData
					postData.data.transport_type = 1
				};
				if (self.week) {
					postData.type = 2
				};
				console.log('postData', postData)
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						var array = self.$Utils.getStorageArray('cartData');
						for (var i = 0; i < orderList.length; i++) {
							for (var j = 0; j < array.length; j++) {
								if (orderList[i].sku_id == array[j].sku[array[j].skuIndex].id) {
									self.$Utils.delStorageArray('cartData', orderList[i], 'id');
								}
							}
						};
						if (self.payType == 2) {
							uni.showToast({
								title: '下单成功',
								duration: 1000,
								success: function() {

								}
							});
							setTimeout(function() {
								self.$Router.redirectTo({
									route: {
										path: '/pages/user-order/user-order?id=1'
									}
								})
							}, 1000);
							return
						};
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
				const postData = self.$Utils.cloneForm(self.pay);
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.orderId
				};
				postData.payAfter = [];
				if (self.logArray.length > 0) {
					for (var i = 0; i < self.logArray.length; i++) {
						postData.payAfter.push({
							tableName: 'Log',
							FuncName: 'add',
							data: {
								type: 1,
								relation_table: 'Order',
								behavior: 0,
								relation_id: self.orderId,
								passage: self.logArray[i],
								thirdapp_id: 2,
								user_no: uni.getStorageSync('user_info').user_no
							},
						});
					}
				};
				if (self.orderLiCurr == 0&&!self.orderInfo.phone) {
					postData.payAfter.push({
						tableName: 'UserInfo',
						FuncName: 'update',
						data: {
							name: self.orderInfo.name,
							phone: self.orderInfo.phone
						},
						searchItem: {
							user_no: uni.getStorageSync('user_info').user_no
						}
					})
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);

						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 1000,
									});
									setTimeout(function() {
										self.$Router.redirectTo({
											route: {
												path: '/pages/user-order/user-order?id=0'
											}
										})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									uni.showToast({
										title: '支付失败',
										duration: 2000,
										icon:'none'
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							uni.showToast({
								title: '支付成功',
								duration: 1000,
							});
							setTimeout(function() {
								self.$Router.redirectTo({
									route: {
										path: '/pages/user-order/user-order?id=0'
									}
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

			getUserData() {
				const self = this;
				const postData = {
					searchItem: {
						thirdapp_id: 2
					}
				};
				postData.tokenFuncName = 'getProjectToken'
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no;
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.userData = res.info.data[0];
						/* self.delivery_fee = uni.getStorageSync('user_info').thirdApp.delivery_fee;
						self.delivery_standard = uni.getStorageSync('user_info').thirdApp.delivery_standard; */
						self.countTotalPrice()
					} else {
						self.$Utils.showToast(res.msg, 'none')
					};
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},

			changeOrderLi(i) {
				const self = this;
				self.orderLiCurr = i;
				self.countTotalPrice()
			},

			getAddressData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					isdefault: 1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.addressData = res.info.data[0];
						self.getStoreData();
					}
				};
				self.$apis.addressGet(postData, callback);
			},

			countTotalPrice() {
				const self = this;
				self.totalPrice = 0;
				self.couponTotalPrice = self.$Utils.addItemInArray(self.pay.coupon, 'price');
				for (var i = 0; i < self.mainData.length; i++) {
					var count = self.mainData[i].count&&parseFloat(self.mainData[i].count)>0?parseInt(self.mainData[i].count):0
					self.totalPrice += self.mainData[i].product.sku[self.mainData[i].skuIndex].price * count;
				}
				self.totalPrice = (parseFloat(self.totalPrice) - parseFloat(self.couponTotalPrice)).toFixed(2);
				
				console.log('self.delivery_standard', self.delivery_standard)
				console.log('self.totalPrice', self.totalPrice, self.shopData)

				/* if(parseFloat(self.delivery_standard)>self.totalPrice&&self.orderLiCurr==1){
					console.log('self.delivery_fee',self.delivery_fee)
					self.delivery = self.delivery_fee;
					self.totalPrice = (parseFloat(self.totalPrice)+parseFloat(self.delivery_fee)).toFixed(2)
				}else{
					self.delivery = 0;
					self.totalPrice = parseFloat(self.totalPrice).toFixed(2)
				}; */
				//console.log('wxPay',wxPay)
				
				if(self.storeData.id){
					if(parseFloat(self.totalPrice)>=parseFloat(self.storeData.info.free)){
						self.is_free = true;
					}else{
						self.is_free = false;
					}
				}
				if(self.is_free){
					self.allPrice = parseFloat(self.totalPrice).toFixed(2);
				}else{
					self.allPrice = (parseFloat(self.totalPrice) + parseFloat(self.f_price)).toFixed(2);
				}
				
				
				if (self.totalPrice > 0) {
					self.pay.wxPay = {
						price: self.orderLiCurr == 1 ? self.allPrice : self.totalPrice,
					};
					// self.pay.other = {
					// 	price: self.orderLiCurr == 1 ? self.allPrice : self.totalPrice,
					// };
				} else {
					delete self.pay.wxPay;
				};
				console.log('pay',self.pay)
			},
		}
	}
</script>

<style>
	.orderList {
		line-height: 60rpx;
		border-radius: 10rpx;
	}

	.orderLi {
		width: 50%;
		text-align: center;
	}

	.orderList .on {
		background-color: #FF6740;
		color: #fff;
	}

	.zt input {
		width: 335rpx;
		line-height: 50rpx;
		border: 1px solid #e1e1e1;
		border-radius: 5rpx;
		height: 50rpx;
	}

	.shopImg {
		width: 183rpx;
		height: 183rpx;
	}

	.shopCon .tit {
		width: 490rpx;
	}

	.carSpan {
		background-color: #FDF7F5;
		line-height: 36rpx;
	}

	.carBot {
		bottom: 0;
	}

	.exec {
		width: 600rpx;
		height: 660rpx;
	}

	.lb {
		width: 251rpx;
		height: 305rpx;
	}

	.btn690 {
		width: 480rpx;
		margin: 0;
	}

	.R-icon {
		margin: 30rpx;
		margin-right: 0;
	}

	.couponShow {
		width: 100%;
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		height: 500rpx;
		z-index: 50;
		padding-bottom: 80rpx;
	}

	.seltIcon {
		width: 36rpx;
		height: 36rpx;
	}

	.black-bj,
	.black-bj2 {
		background: #000;
		opacity: 0.5;
		position: fixed;
		left: 0;
		top: 0;
		right: 0;
		bottom: 0;
		z-index: 40;
	}
	
	.num{width: 80rpx;}
</style>
