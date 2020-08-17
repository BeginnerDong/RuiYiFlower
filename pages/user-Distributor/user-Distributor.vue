<template>
	<view>
		<view class="font-28 color2 d-flex bg-white shadow mb-2 list">
			<view class="li" :class="current==1?'on':''" @click="change(1)">全部</view>
			<view class="li" :class="current==2?'on':''" @click="change(2)">待配送</view>
			<view class="li" :class="current==3?'on':''" @click="change(3)">配送中</view>
			<view class="li" :class="current==4?'on':''" @click="change(4)">已配送</view>
		</view>
		
		<view class="color2 font-24 mx-3 bg-white radius10 mb-2" v-for="(item,index) in mainData" :key="index">
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="color6">订单编号：{{item.order_no}}</view>
				<view class="Mcolor" v-if="item.transport_status==0">待配送</view>
				<view class="Mcolor" v-if="item.transport_status==1">配送中</view>
				<view class="Mcolor" v-if="item.transport_status==2">已完成</view>
			</view>
			<view class="d-flex j-sb a-center p-2 bB-f5">
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
				<view class="d-flex a-center">支付方式：<text class="red">{{item.pay_type==1?'线上支付':'线下支付'}}</text></view>
				<view>{{item.snap_address.name?item.snap_address.name:''}} {{item.snap_address.phone?item.snap_address.phone:''}}</view>
			</view>
			<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
				<view class="d-flex a-center">订单类型：<text class="red">{{item.type==2?'包月':'普通'}}</text></view>
			</view>
			<view class="d-flex j-end px-2">
				<view class="tkBtn b-e1 my-3 radius10" v-if="item.transport_status==0" @click="orderUpdate(index,1)">立即配送</view>
				<view class="tkBtn b-e1 my-3 radius10" v-if="item.transport_status==1" @click="orderUpdate(index,2)">配送完成</view>
				<view class="tkBtn b-e1 my-3 radius10" v-if="item.transport_status==2&&item.pay_type==2&&item.pay_status==0">上传支付凭证</view>
			</view>
		</view>
		
		
		<view style="height: 120rpx;"></view>
		<view class="py-3 bT-f5 p-f bottom-0 left-0 right-0 text-center bg-white dis"  @click="loginOff">退出登录</view>
		
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
					//pay_status:1,
					level:1,
					transport_type:1,
					order_step:0
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			// self.searchItem.shop_no = uni.getStorageSync('riderInfo').user_no;
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
			
			upLoadImg(index) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.payComplete(res.info.url,index)
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 1,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths[0];
						var file = res.tempFiles[0];
						var obj = res.tempFiles[0].path.lastIndexOf(".");
						var ext = res.tempFiles[0].path.substr(obj+1);
						console.log(callback)
						self.$Utils.uploadFile(tempFilePaths, 'file', {
							tokenFuncName: 'getRiderToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
						}, callback)
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
			payComplete(url,index) {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getRiderToken';
				postData.data = {
					pay_status:1,
					mainImg:[{url:url,type:'image'}]
				};
				postData.searchItem = {
					id:self.mainData[index].id,
					user_type:0
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
			
			orderUpdate(index,type) {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getRiderToken';
				postData.data = {
					transport_status:type
				};
				postData.searchItem = {
					id:self.mainData[index].id,
					user_type:0
				};
				if(self.mainData[index].type==2&&type==2){
					self.thisIndex = []
					for (var i = 0; i < self.mainData[index].log.length; i++) {
						if(self.mainData.log[i].behavior==0){
							self.thisIndex.push(i);
							//return
						}
					};
					if(self.thisIndex.length>0){
						postData.saveAfter = [{
							tableName: 'Log',
							FuncName: 'update',
							data: {
								behavior:1,
							},
							searchItem:{
								id:self.mainData[index].log[self.thisIndex[0]].id,
								user_type:0
							}
						}]
					}else{
						postData.data.transport_status = type
					}
				}else{
					postData.data.transport_status = type
				}
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
			
			loginOff(){
				const self = this;
				uni.removeStorageSync('riderInfo');
				uni.removeStorageSync('riderToken');
				self.Router.redirectTo({route:{path:'/pages/user/user'}})
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
						self.searchItem.transport_status = 1
					}else if(self.current==4){
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
				postData.tokenFuncName = 'getRiderToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
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
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					//self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	};
</script>

<style>
.li{width: 25%;}
.orderImg{width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.tkBtn{width: 140rpx;line-height: 54rpx;text-align: center;}
.dis{height: 100rpx;}
</style>
