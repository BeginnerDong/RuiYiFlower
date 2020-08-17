<template>
	<view>
		
		<view class="color2 font-24 m-2 bg-white radius10">
				<view class="bB-f5 py-3 px-2 d-flex j-sb a-center">
					<view class="color6">订单编号：{{mainData.order_no?mainData.order_no:''}}</view>
					<view class="color9">{{mainData.create_time?mainData.create_time:''}}</view>
				</view>
				<view class="d-flex j-sb a-center p-2 bB-f5" :data-id="item.id" >
					<image :src="mainData.orderItem&&mainData.orderItem[0]&&mainData.orderItem[0].snap_product
							&&mainData.orderItem[0].snap_product.product.mainImg&&mainData.orderItem[0].snap_product.product.mainImg[0]?mainData.orderItem[0].snap_product.product.mainImg[0].url:''" class="orderImg"></image>
					<view class="flex-1 pl-3 py-1 d-flex flex-column j-sb txt">
						<view>{{mainData.orderItem&&mainData.orderItem[0]&&mainData.orderItem[0].snap_product
							?mainData.orderItem[0].snap_product.product.title:''}}</view>
						<view class="price font-32">{{mainData.price?mainData.price:''}}</view>
					</view>
				</view>
				<view class="py-3 px-2">
					<textarea v-model="submitData.description" placeholder="请填写商品评论,让更多人知道" />
					
					<view class="pb-2">添加图片</view>
					<view class="d-flex" style="flex-wrap: wrap;">
						<image class="wh120" style="margin-bottom: 20rpx;"  v-for="(item,index) in submitData.mainImg" :src="item.url" :key="index" mode=""></image>
						<image @click="upLoadImg('mainImg')" style="margin-bottom: 20rpx;" src="../../static/images/icon5.png" class="wh120" v-if="submitData.mainImg.length<9"></image>
					</view>
					
					<view class="btn690"  @click="Utils.stopMultiClick(submit)">提交</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				mainData:{},
				submitData: {
					order_no: '',
					product_no: '',
					description: '',
					type:1,
					title:'',
					headImg :[],
					//passage1:'',
					mainImg:[],
					thirdapp_id:2
				},
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			var res = self.$Token.getProjectToken(function(){
				self.$Utils.loadAll(['getMainData'], self)
			});
			if(res){
				self.$Utils.loadAll(['getMainData'], self)
			};
			self.submitData.headImg  = [{type:'image',url:uni.getStorageSync('user_info').headImgUrl}];
			self.submitData.title = uni.getStorageSync('user_info').nickname
		},
		
		methods: {
			
			
			upLoadImg(type) {
				const self = this;	
				if (self.submitData[type].length > 8) {
					api.showToast('仅限9张', 'fail');
					return;
				};
				wx.showLoading({
					mask: true,
					title: '上传中',
				});
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log('type',type)
						console.log(self.submitData)
						wx.hideLoading()
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				wx.chooseImage({
					count: 9,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths;
						console.log(callback)
						for (var i = 0; i < tempFilePaths.length; i++) {
							var file = res.tempFiles[i];
							var obj = res.tempFiles[i].path.lastIndexOf(".");
							var ext = res.tempFiles[i].path.substr(obj+1);
							self.$Utils.uploadFile(tempFilePaths[i], 'file', {
								tokenFuncName: 'getProjectToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'img'
							}, callback)
						}
					},
					fail: function(err) {
						wx.hideLoading();
					},			
				})			
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				postData.getAfter = {
					orderItem:{
						tableName:'OrderItem',
						middleKey:'order_no',
						key:'order_no',
						searchItem:{
							status:1
						},
						condition:'=',
						
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.submitData.order_no = self.mainData.order_no;
						//self.submitData.passage1 = self.mainData.parent_no;
						self.submitData.product_no = self.mainData.type==1?self.mainData.orderItem[0].snap_product.product.product_no:self.mainData.orderItem[0].snap_product.product_no
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				var newObject = self.$Utils.cloneForm(self.submitData);
				delete newObject.headImg ;
				delete newObject.title;
				delete newObject.mainImg;
				const pass = self.$Utils.checkComplete(newObject);
				console.log('pass', pass);
				console.log('self.submitData', self.submitData)
				if (pass) {
					self.messageAdd();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			messageAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				postData.saveAfter = [{
				  tableName:'Order',
				  FuncName:'update',
				  searchItem:{
				    id:self.id
				  },
				  data:{
				    isremark:1,
				  }
				}];
				const callback = (data) => {
			
					if (data.solely_code == 100000) {
			
						self.$Utils.showToast('评价成功', 'none')
						setTimeout(function() {
							self.$Router.redirectTo({route:{path:'/pages/userOrder/userOrder'}})
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}
			
				};
				self.$apis.messageAdd(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
	textarea{display: block;width: 100%;}
.btn690{width: 100%;margin: 220rpx 0 20rpx;}
.orderImg {width: 125rpx;height: 125rpx;border-radius: 10rpx;margin-right: 20rpx;}
.txt{height: 125rpx;}
</style>
