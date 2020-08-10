<template>
	<view>
		
		<view class="bg-white py-3 px-2 mx-3 my-2 radius10 overflow-h line-h d-flex a-center j-sb p-r mb-2">
			<view class="font-26">
				<view class="pb-3 color9">客户信息</view>
				<view>{{mainData.name?mainData.name:''}} {{mainData.phone?mainData.phone:''}}</view>
			</view>
			<image src="../../static/images/the orderl-icon.png" class="zt-icon p-a top-0 left-0 right-0"></image>
		</view>
		
		<view class="p-2 d-flex a-center j-sb bg-white mx-3" v-for="(item,index) in mainData.child" :key="index">
			<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product&&item.orderItem[0].snap_product.product&&
								item.orderItem[0].snap_product.product.mainImg&&item.orderItem[0].snap_product.product.mainImg[0]?item.orderItem[0].snap_product.product.mainImg[0].url:''" class="shopImg"></image>
			<view class="shopCon d-flex flex-column">
				<view class="tit avoidOverflow pb-2">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product?item.orderItem[0].snap_product.title:''}}</view>
				<!-- <view class="d-flex"><view class="font-24 carSpan mb-5 color6 px-1">精品大束</view></view> -->
				<view class="flex1">
					<view class="price">{{item.price}}</view>
					<view class="font-26 color6">x{{item.count}}</view>
				</view>
			</view>
		</view>
		
		<view class="bg-white mx-3 radius10 mt-2 font-24 color9 px-2 pb-3" v-if="mainData.type==2">
			<view class="flex1 py-3 bB-f5 color2 mb-3">
				<view>包月详情</view>
			</view>
			<view class="flex1 pb-3"  v-for="(item,index) in mainData.log" :key="index">
				<view class="">第{{index+1}}次收花时间：{{Utils.timeto(parseInt(item.passage)*1000,'ymd')}}</view>
				<view><text class="red font-28">{{item.behavior==1?'已核销':'未核销'}}</text></view>
			</view>
		</view>
		
		<view class="btnBox">
			<view class="btn690" v-if="mainData.transport_status==0" @click="orderUpdate(mainData.id)">确认核销</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				
				mainData:{},
				name:'',
				address:'',
				Utils:this.$Utils
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.name = uni.getStorageSync('staffInfo').info.name;
			self.address = uni.getStorageSync('staffInfo').info.address;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					id:self.id,
					user_type:0
				};
				postData.getAfter = {
					log:{
						tableName:'Log',
						middleKey:'id',
						key:'relation_id',
						searchItem:{
							status:1,
							user_type:0
						},
						condition:'='
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.thisIndex = []
						for (var i = 0; i < self.mainData.log.length; i++) {
							if(self.mainData.log[i].behavior==0){
								self.thisIndex.push(i);
								//return
							}
						}
					};
					console.log('self.thisIndex', self.thisIndex)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
			orderUpdate(id) {
				const self = this;
				uni.setStorageSync('canClick', false);
				uni.showModal({
				    title: '提示',
				    content: '确定要核销此订单吗',
					confirmColor:'#db1b1b',
				    success: function (res) {
				        if (res.confirm) {
				            const postData = {};
				            postData.tokenFuncName = 'getStaffToken';
				            postData.data = {};
				            postData.searchItem = {
				            	id:id,
				            	user_type:0
				            };
							if(self.mainData.type==2){
								if(self.thisIndex.length>0){
									postData.saveAfter = [{
										tableName: 'Log',
										FuncName: 'update',
										data: {
											behavior:1,
										},
										searchItem:{
											id:self.mainData.log[self.thisIndex[0]].id,
											user_type:0
										}
									}]
								}else{
									postData.data.transport_status = 2
								}
							}else{
								postData.data.transport_status = 2
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
				        } else if (res.cancel) {

				        }
				    }
				});
				
			 },
			
		}
	};
</script>

<style>
.shopCon .tit{width: 455rpx;}
.btnBox{padding-top: 220rpx;}
</style>
