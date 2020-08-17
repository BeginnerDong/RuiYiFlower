<template>
	<view>

		<view class="font-26 color2 mx-3 my-2 bg-white d-flex overflow-h orderList">
			<view class="orderLi" :class="orderLiCurr==0?'on':''" @click="changeOrderLi(0)">门店自提({{userData.order.zt?userData.order.zt:0}})</view>
			<view class="orderLi bL-f5 bR-f5" :class="orderLiCurr==1?'on':''" @click="changeOrderLi(1)">送货上门({{userData.order.sh?userData.order.sh:0}})</view>
			<view class="orderLi" :class="orderLiCurr==2?'on':''" @click="changeOrderLi(2)">包月订单({{userData.order.by?userData.order.by:0}})</view>
		</view>

		<!-- 自提门店 -->
		<view v-show="orderLiCurr==0">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li1" :class="status==0?'on':''" @click="changeStatus(0)">全部</view>
				<view class="li li1" :class="status==1?'on':''" @click="changeStatus(1)">待提货</view>
				<view class="li li1" :class="status==2?'on':''" @click="changeStatus(2)">已提货</view>
				<view class="li li1" :class="status==3?'on':''" @click="changeStatus(3)">退款售后</view>
			</view>

			<!-- 待提货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2" v-for="(item,index) in mainData" :key="index">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：{{item.order_no}}</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==0&&item.order_step==0">待提货</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==2&&item.order_step==0">已提货</view>
					<view class="Mcolor" v-if="item.order_step>0">已退款</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-orderDetail/user-orderDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="d-flex a-center">
						<image v-for="(c_item,c_index) in item.child" :key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''"
						 class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon m-2" 
					></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">{{item.create_time}}</view>
					<view>供{{item.child.length}}件商品 合计：￥{{item.price}}</view>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="d-flex a-center" v-if="item.pay_status==1&&item.transport_status==0&&item.order_step==0">
						<view>提货码：</view>
						<image :src="item.qrcode" @click="hxEwmShow(index)" class="hx-icon"></image>
					</view>
					<view class="tkBtn b-e1 radius10" v-if="item.transport_status==0&&item.order_step==0"
					 :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-refund/user-refund?id='+$event.currentTarget.dataset.id}})">申请退款</view>
				</view>
			</view>
		</view>

		<!-- 送货上门 -->
		<view v-show="orderLiCurr==1">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li2" :class="statusTwo==0?'on':''" @click="changeStatusTwo(0)">全部</view>
				<view class="li li2" :class="statusTwo==1?'on':''" @click="changeStatusTwo(1)">待送货</view>
				<view class="li li2" :class="statusTwo==2?'on':''" @click="changeStatusTwo(2)">送货中</view>
				<view class="li li2" :class="statusTwo==3?'on':''" @click="changeStatusTwo(3)">已完成</view>
				<view class="li li2" :class="statusTwo==4?'on':''" @click="changeStatusTwo(4)">退款售后</view>
			</view>

			<!-- 已发货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2" v-for="(item,index) in mainData" :key="index">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：{{item.order_no}}</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==0&&item.order_step==0">待送货</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==1&&item.order_step==0">送货中</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==2&&item.order_step==0">已完成</view>
					<view class="Mcolor" v-if="item.order_step>0">已退款</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-orderDetail/user-orderDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="d-flex a-center">
						<image v-for="(c_item,c_index) in item.child" :key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''"
						 class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">{{item.create_time}}</view>
					<view>供{{item.child.length}}件商品 合计：￥{{item.price}}</view>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="d-flex a-center">支付方式：{{item.pay_type==1?'线上支付':'线下支付'}}</view>
					<view class="tkBtn b-e1 radius10" v-if="item.transport_status==0&&item.order_step==0&&item.pay_type==1&&item.pay_status==1"
					:data-id="item.id" 
					@click="Router.navigateTo({route:{path:'/pages/user-refund/user-refund?id='+$event.currentTarget.dataset.id}})">申请退款</view>
					<view class="tkBtn b-e1 radius10" v-if="item.pay_status==0" @click="orderUpdate(index,1)"
					>取消订单</view>
					<view class="tkBtn b-e1 radius10" v-if="item.pay_status==1&&item.transport_status==1&&item.order_step==0" @click="orderUpdate(index,2)"
					>确认收货</view>
				</view>
			</view>


		</view>

		<!-- 包月订单 -->
		<view v-show="orderLiCurr==2">
			<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
				<view class="li li3" :class="statusThree==0?'on':''" @click="changeStatusThree(0)">全部</view>
				<view class="li li3" :class="statusThree==1?'on':''" @click="changeStatusThree(1)">进行中</view>
				<view class="li li3" :class="statusThree==2?'on':''" @click="changeStatusThree(2)">已完成</view>
			</view>

			<!-- 已收货 -->
			<view class="color2 font-24 mx-3 bg-white radius10 mb-2" v-for="(item,index) in mainData" :key="index">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：{{item.order_no}}</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==0&&item.order_step==0">进行中</view>
					<view class="Mcolor" v-if="item.pay_status==1&&item.transport_status==2&&item.order_step==0">已完成</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-orderDetail/user-orderDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="d-flex a-center">
						<image v-for="(c_item,c_index) in item.child" :key="c_index" :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''"
						 class="orderImg"></image>
					</view>
					<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color9">{{item.create_time}}</view>
					<!-- <view>供3件商品 合计：￥56</view> -->
					
				</view>
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center" v-if="item.transport_type==2">
					<view class="d-flex a-center">
						<view>提货码：</view>
						<image :src="item.qrcode" @click="hxEwmShow(index)" class="hx-icon"></image>
					</view>
					<view class="tkBtn b-e1 radius10" style="width: 190rpx;"
					 :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-orderDetail/user-orderDetail?id='+$event.currentTarget.dataset.id}})">查看包月详情</view>
				</view>
			</view>

		</view>

		<view class="black-bj" v-show="is_hxEwmShow"></view>
		<view class="hxEwmShow" v-show="is_hxEwmShow">
			<view>
				<image class="ewm" :src="mainData[chooseIndex].qrcode" mode=""></image>
			</view>
			<view class="closeBtn" @click="hxEwmShow">×</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				orderLiCurr: -1,
				liCurr: 0,
				status: 0,
				mainData: [],
				searchItem: {
					level: 1,
					transport_type: 2,
					pay_status: 1,
					type: 1
				},
				statusTwo: 0,
				statusThree: 0,
				chooseIndex: -1,
				is_hxEwmShow:false,
				userData:{}
			}
		},



		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getUserData'], self);
			if(options.id){
				self.optionsId = options.id
			}
		},

		onShow() {
			const self = this;
			if(self.optionsId){
				self.changeOrderLi(self.optionsId)
			}
		},

		methods: {
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.getAfter = {
					order: {
						tableName: 'Order',
						searchItem:{
							status:1
						},
						middleKey: 'user_no',
						key: 'user_no',
						condition: 'in',
						compute:{
						  zt:[
						    'count',
						    'count',
						    {level: 1,
							transport_type: 2,
							pay_status: 1,
							type: 1}
						  ],
						  sh:[
						    'count',
						    'count',
						    {level: 1,
							transport_type: 1,
							//pay_status: 1,
							type: 1}
						  ],
						  by:[
						    'count',
						    'count',
						    {level: 1,
							pay_status: 1,
							type: 2}
						  ],
						},
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
					}
					
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			orderUpdate(index,type) {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					
				};
				if(type==1){
					postData.data.status=-1
				}else{
					postData.data.transport_status=2
				};
				postData.searchItem = {
					id:self.mainData[index].id,
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },

			hxEwmShow(index) {
				const self = this;

				if (index || index == 0) {
					self.chooseIndex = index
				};
				self.is_show = !self.is_show
				self.is_hxEwmShow = !self.is_hxEwmShow
			},

			changeOrderLi(i) {
				const self = this;
				if (self.orderLiCurr != i) {
					self.status = 0;
					self.statusTwo = 0;
					self.statusThree = 0;
					self.orderLiCurr = i
					if (self.orderLiCurr == 0) {
						self.searchItem = {
							level: 1,
							transport_type: 2,
							pay_status: 1,
							type: 1
						}
					} else if (self.orderLiCurr == 1) {
						self.searchItem = {
							level: 1,
							transport_type: 1,
							//pay_status: 1,
							type: 1
						}
					} else {
						self.searchItem = {
							level: 1,
							pay_status: 1,
							type: 2
						}
					};
					self.getMainData(true)
				}
			},

			changeLi(i) {
				const self = this;
				self.liCurr = i
			},

			changeStatus(status) {
				const self = this;
				if (self.status != status) {
					self.status = status;
					if (self.status == 0) {
						delete self.searchItem.transport_status;
						delete self.searchItem.order_step
					} else if (self.status == 1) {
						self.searchItem.transport_status = 0;
						self.searchItem.order_step = 0
					} else if (self.status == 2) {
						self.searchItem.transport_status = 2;
						self.searchItem.order_step = 0
					} else if (self.status == 3) {
						delete self.searchItem.transport_status;
						self.searchItem.order_step = ['>', 0]
					};
					self.getMainData(true)
				}
			},

			changeStatusThree(status) {
				const self = this;
				if (self.statusThree != status) {
					self.statusThree = status;
					if (self.statusThree == 0) {
						delete self.searchItem.transport_status;
						delete self.searchItem.order_step
					} else if (self.statusThree == 1) {
						self.searchItem.transport_status = 0;
						self.searchItem.order_step = 0
					} else if (self.statusThree == 2) {
						self.searchItem.transport_status = 2;
						self.searchItem.order_step = 0
					}
					self.getMainData(true)
				}
			},


			changeStatusTwo(status) {
				const self = this;
				if (self.statusTwo != status) {
					self.statusTwo = status;
					if (self.statusTwo == 0) {
						delete self.searchItem.transport_status;
						delete self.searchItem.order_step
					} else if (self.statusTwo == 1) {
						self.searchItem.transport_status = 0;
						self.searchItem.order_step = 0
					} else if (self.statusTwo == 2) {
						self.searchItem.transport_status = 1;
						self.searchItem.order_step = 0
					} else if (self.statusTwo == 3) {
						self.searchItem.transport_status = 2;
						self.searchItem.order_step = 0
					} else if (self.statusTwo == 4) {
						delete self.searchItem.transport_status;
						self.searchItem.order_step = ['>', 0]
					}
					self.getMainData(true)
				}
			},

			getMainData(isNew) {
				const self = this;
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
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no;
				if(self.orderLiCurr==2){
					postData.getAfter = {
						log:{
							tableName:'Log',
							middleKey:'id',
							key:'relation_id',
							searchItem:{
								status:1,
							},
							condition:'='
						}
					};
				}
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
		}
	}
</script>

<style>
	.black-bj {background: #000;opacity: 0.5;position: fixed;left: 0;top: 0;right: 0;bottom: 0;z-index: 40; }
	.orderList {
		line-height: 70rpx;
		border-radius: 35rpx;
	}

	.orderLi {
		width: 33.33%;
		text-align: center;
	}

	.orderList .on {
		background-color: #FF6740;
		color: #fff;
	}

	.li1 {
		width: 25%;
	}

	.li2 {
		width: 20%;
	}

	.li3 {
		width: 33.33%;
	}

	.orderImg {
		width: 125rpx;
		height: 125rpx;
		border-radius: 10rpx;
		margin-right: 20rpx;
	}

	.tkBtn {
		width: 140rpx;
		line-height: 54rpx;
		text-align: center;
	}

	.hxEwm {
		width: 80rpx;
		height: 80rpx;
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
