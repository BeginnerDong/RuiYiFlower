<template>
	<view class="line-h color2">
		<!-- banner -->
		<view class="banner p-r">
			<view class="back mt-3" @click="Router.back(1)">
				<image src="../../static/images/back-icon.png" mode=""></image>
			</view>
			<swiper class="swiper-box" indicator-dots="indicatorDots" :autoplay="autoplay"  interval="3000" indicator-active-color="#FF6F48">
				<block>
					<swiper-item class="swiper-item" v-for="(item,index) of mainData.bannerImg" :key="index">
						<image v-if="item.type=='image'" :src="item.url"
						 mode="slide-image" />
						<video style="height: 750rpx;width: 750rpx;" id="myVideo" loop  show-play-btn controls @click="ZhanTing"  objectFit="cover" v-if="item.type=='vedio'"
						 :src="item.url"></video>
					</swiper-item>			
				</block>
			</swiper>
		</view>
		<view class="bg-white mb-2 py-2 px-3"  v-if="mainData.type==4">
			<view class="d-flex a-center font-w" style="color: #FF6740;">
				<view class="colorM">距结束仅剩:</view>
				<view class="pl-2">{{mainData.day?mainData.day:'00'}}天</view>
				<view class="colorM">{{mainData.hourCount?mainData.hourCount:'00'}}:{{mainData.minCount?mainData.minCount:'00'}}:{{mainData.secCount?mainData.secCount:'00'}}</view>
			</view>
		</view>
		<view class="bg-white p-3 d-flex j-sb mb-2">
			<view class="font-w">
				<view class="font-32 pb-4">{{mainData.title}}</view>
				
				<view class="font-30 price">{{mainData.price}}</view>
			</view>
			<view class="text-center">
				<button open-type="share" style="background:#fff;line-height:1.5" class="font-24 color6 d-flex pl-3 bL-f5"><image src="../../static/images/detailsl-icon.png" class="fx-icon"></image>分享</button style="background:#fff;line-height:1.5">
				<view class="font-22 color9 pt-5 pl-3">销量:{{mainData.sale_count?mainData.sale_count:0}}</view>
			</view>
		</view>
		
		<view class="bg-white px-3 mb-2">
			<view class="pt-3 pb-4 bB-f5 d-flex a-center">
				<view class="font-28 color6">配送</view>
				<view class="font-24 color2 d-flex">
					<view class="pl-3 d-flex"><image src="../../static/images/detailsl-icon1.png" class="ps-icon"></image>送货上门</view>
					<view class="pl-3 d-flex"><image src="../../static/images/detailsl-icon1.png" class="ps-icon"></image>到店自提</view>
				</view>
			</view>
			<!-- <view class="py-3 d-flex a-center">
				<view class="font-28 color6">运费</view>
				<view style="line-height: 40rpx;">
					<view class="font-24 color2 pl-3">送货上门需运费￥{{deliver}}(满￥{{delivery_standard}}免配送费) </view>
					<view class="font-24 color2 pl-3">到店自提免费</view>
				</view>
			</view> -->
		</view>
		
		<view class="p-3 d-flex a-center bg-white mb-2">
			<view class="font-28 color6">规格</view>
			<view class="font-24 color2 flex-1 d-flex j-sb pl-3" @click="ggShow">
				<view class="flex-1">{{mainData.sku[specsCurr]?'已选:'+mainData.sku[specsCurr].title:'请选择'}}</view>
				<image src="../../static/images/detailsl-icon2.png" class="R-icon"></image>
			</view>
		</view>
		
		<view class="p-3 bg-white mb-2">
			<view class="font-28 color6 pb-3">服务说明</view>
			<view class="font-24 color2 line-h-md">
				{{mainData.description}}
			</view>
		</view>
		
		<view class="p-3 bg-white pb-5">
			<view class="font-28 color6 pb-3 d-flex cardBox">
				<view class="mr-5 pb-2 card" @click="changeCard(0)" :class="titCard==0?'on':''">商品描述</view>
				<view class="mr-5 pb-2 card" @click="changeCard(1)" :class="titCard==1?'on':''">商品评论</view>
			</view>
			<view class="font-24 color2">
				<!-- 描述 -->
				<view class="content ql-editor line-h-md text-center ms" style="padding:0" v-html="mainData.content" v-show="titCard==0">
				</view>
				
				<!-- 评论 -->
				<view v-show="titCard==1" v-if="messageData.length>0" v-for="(item,index) in messageData" :key="index">
					<view class="bB-f5 py-2">
						<view class="d-flex a-center j-sb">
							<view class="d-flex a-center">
								<image :src="item.headImg!=''?item.headImg:'../../static/images/head.png'" 
								class="wh60 mr-3 radius-5"></image>
								<view>{{item.nickname!=''?item.title:'用户'}}</view>
							</view>
							<view class="color6">{{item.create_time?item.create_time:''}}</view>
						</view>
						<view>
							<view class="py-2">{{item.description}}</view>
							<view class="d-flex" style="flex-wrap: wrap;">
								<image v-for="(c_item,c_index) in item.mainImg" :key="c_index" :src="c_item.url" class="wh120"></image>
							</view>
						</view>
					</view>
					<view v-if="messageData.length==0" style="width: 100%;text-align: center;">暂无评论~</view>
				</view>
				
			</view>
		</view>
		
		<view style="height: 100rpx;"></view>
		<view class="text-center colorf font-30 p-f bottom-0 left-0 right-0 d-flex bT-f5">
			<view class="flex-1 bg-white pt-2" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/detailsl-icon3.png" class="fh-icon"></image>
				<view class="font-24 color6 pt-1">首页</view>
			</view>
			<button class="flex-1 bg-white pt-2" open-type="contact" style="line-height: 1;">
				<image src="../../static/images/kefu-detail.png" style="width: 40rpx;height: 40rpx;margin: auto;"></image>
				<view class="font-24 color6" style="padding-top: 3rpx;">客服</view>
			</button>
			<view class="btn" style="background-color: #FF6740;" v-if="mainData.type==1&&mainData.sell_out==0"  @click="ggShow">加入购物车</view>
			<view class="btn" :style="mainData.type==2||mainData.type==4?'width:560rpx':''" v-if="mainData.sell_out==0"  @click="ggShow">立即购买</view>
			<view class="btn" style="width: 560rpx;background-color: #666;" v-if="mainData.sell_out==1">已售罄</view>
		</view>
		
		<!-- 规格 -->
		<view class="bg-mask line-h" v-show="gg_show">
			<view class="radius20-T bg-white p-a bottom-0 left-0 right-0 p-3 d-flex flex-column ggBox">
				<view class="d-flex j-sb bB-f5 pb-3">
					<view class="gg radius20 overflow-h" @click="preview()"><image :src="mainData.sku[specsCurr]&&mainData.sku[specsCurr].mainImg&&mainData.sku[specsCurr].mainImg[0]
					?mainData.sku[specsCurr].mainImg[0].url:''"></image></view>
					<view class="pl-2 flex-1">
						<view class="font-36 price pb-3">{{mainData.sku[specsCurr]?mainData.sku[specsCurr].price:''}}</view>
						<view class="font-24 color9">库存：{{mainData.sku[specsCurr]?mainData.sku[specsCurr].stock:'0'}}</view>
					</view>
					<view @click="ggShow">
						<image src="../../static/images/detailsl-icon4.png" class="x-icon"></image>
					</view>
				</view>
				
				<view class="flex-1 flexY flex-column mb-3 ggPartBox">
					<view class="ggPart bB-f5 pb-1" v-for="(item,index) in labelData" :key="index" v-if="item.id!=99">
						<view class="font-26 color2 py-3">{{item.title}}</view>
						<view class="font-24 color6">
							<view class="span"  v-for="(c_item,c_index) in item.children" 
						style="display: inline-block;"
						 :class="Utils.inArray(c_item.id,choose_sku_item)==-1?'cantChoose'
						 :(Utils.inArray(c_item.id,sku_item)!=-1?'on':'')"
						  :key="c_index" :data-c_id="c_item.id" :data-id="item.id"
						@click="Utils.inArray($event.currentTarget.dataset.c_id,choose_sku_item)!=-1?
						chooseSku($event.currentTarget.dataset.id,$event.currentTarget.dataset.c_id):''">{{c_item.title}}</view>
						</view>
					</view>
					<view class="ggPart pb-1" v-if="mainData.type==2">
						<view class="font-26 color2 py-3">配送星期</view>
						<view class="font-24 color6">
							<view class="span" @click="chooseWeekFunc(index)" :class="chooseWeek==index?'on':''" v-for="(item,index) in week" :key="index">{{item.key}}</view>
						</view>
					</view>
				</view>
				
				<view class="font-30 colorf text-center d-flex pb-3">
					<view class="radiusL-4 ggBtn" v-if="mainData.type==1&&mainData.sell_out==0"  @click="addCar">加入购物车</view>
					<view class="ggBtn" :class="mainData.type==1?'radiusR-4':''" :style="mainData.type==2||mainData.type==4?'width:690rpx':''"
					 @click="Utils.stopMultiClick(goBuy)" v-if="mainData.sell_out==0">立即购买</view>
					 <view class="btn" style="width: 690rpx;background-color: #666;" v-if="mainData.sell_out==1">已售罄</view>
					 
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import Vue from 'vue'
	export default {
		
		data() {
			return {
				Router:this.$Router,
				gg_show:false,
				mainData:{},
				labelData:[],
				skuData:[],
				specsCurr:0,
				sku_item:[],
				choose_sku_item:[],
				Utils:this.$Utils,
				week:[{value:0,key:'周日收花'},{value:1,key:'周一收花'},{value:2,key:'周二收花'},{value:3,key:'周三收花'},{value:4,key:'周四收花'},{value:5,key:'周五收花'},
				{value:6,key:'周六收花'},],
				chooseWeek:-1,
				deliver:0,
				titCard:0,
				messageData:[],
				delivery_standard:0,
				autoplay:true
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.id = options.id;
			if (options.user_no) {
				const callback = (res) => {
					
					self.getMainData();
					self.deliver = uni.getStorageSync('user_info').thirdApp.delivery_fee;
					self.delivery_standard = uni.getStorageSync('user_info').thirdApp.delivery_standard;
				};
				self.$Token.getProjectToken(callback, {
					refreshToken: true,
					parent_no: options.user_no
				})
			} else {
				const callback = (res) => {
					self.getMainData();
					self.deliver = uni.getStorageSync('user_info').thirdApp.delivery_fee;
					self.delivery_standard = uni.getStorageSync('user_info').thirdApp.delivery_standard;
				};
				self.$Token.getProjectToken(callback, {
					refreshToken: true,
				})
			}
			
		},
		
		onShow() {
			const self = this;
			self.orderList = [];
			uni.removeStorageSync('payPro');
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')&&self.curr==2) {
				self.paginate.currentPage++;
				self.getMessageData()
			};
		},
		
		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				return {
					title:self.mainData.title,
					path: '/pages/goodsDetail/goodsDetail?user_no='+uni.getStorageSync('user_info').user_no+'&id='+self.id, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
				}
			}else{
				return {
					title:self.mainData.title,
					path: '/pages/goodsDetail/goodsDetail?user_no='+uni.getStorageSync('user_info').user_no+'&id='+self.id, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
				}
			}
		},
		
		methods: {
			
			preview(){
				const self = this;
				uni.previewImage({
					urls:[self.mainData.sku[self.specsCurr]&&self.mainData.sku[self.specsCurr].mainImg&&self.mainData.sku[self.specsCurr].mainImg[0]
					?self.mainData.sku[self.specsCurr].mainImg[0].url:'']
				})
			},
			
			ZhanTing() {
				const self = this;
				self.autoplay = !self.autoplay
			},
			
			changeCard(i){
				const self = this;
				self.titCard = i;
			},
			
			chooseWeekFunc(index){
				const self = this;
				self.chooseWeek = index;
			},
			
			ggShow(){
				const self = this;
				self.gg_show = !self.gg_show
			},
			
			getMainData() {
				const self = this;
				/* var path = '/pages/goodsDetail/goodsDetail?user_no='+uni.getStorageSync('user_info').user_no+'&id='+self.id; */
				/* console.log('path',path) */
				const postData = {};
				postData.searchItem = {
					thirdapp_id:2,
					id:self.id
				};
				postData.getAfter = {
					sku: {
						tableName: 'Sku',
						middleKey: 'product_no',
						key: 'product_no',
						condition: '=',
						searchItem: {
							status: 1
						}
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						if(self.mainData.type==4){
							let time = self.mainData.end_time/1000 - Date.parse(new Date()) / 1000;
							console.log(time)
							
							self.interval = setInterval(function() {
								time--; //每执行一次让倒计时秒数减一
								var day = Math.floor( time/ (24*3600) ); // Math.floor()向下取整 
								var hourCount = Math.floor( (time - day*24*3600) / 3600);
								var minCount = Math.floor( (time - day*24*3600 - hourCount*3600) /60 );
								var secCount = time - day*24*3600 - hourCount*3600 - minCount*60; 
								if (day >= 0 && day <= 9) {
									day = "0" + day;
								};
								if (hourCount >= 0 && hourCount <= 9) {
									hourCount = "0" + hourCount;
								}
								if (minCount >= 0 && minCount <= 9) {
									minCount = "0" + minCount;
								}
								if (secCount >= 0 && secCount <= 9) {
									secCount = "0" + secCount;
								}
								Vue.set(self.mainData,'day',day)
								Vue.set(self.mainData,'hourCount',hourCount)
								Vue.set(self.mainData,'minCount',minCount)
								Vue.set(self.mainData,'secCount',secCount)
								//如果当秒数小于等于0时 停止计时器 且按钮文字变成重新发送 且按钮变成可用状态 倒计时的秒数也要恢复成默认秒数 即让获取验证码的按钮恢复到初始化状态只改变按钮文字
								if (time <= 0) {
									clearInterval(self.interval)
								}
							}, 1000);
						};
						for(var key in self.mainData.label){
						  if(self.mainData.sku_array.indexOf(parseInt(key))!=-1){
						    self.labelData.push(self.mainData.label[key])
						  };    
						};
						console.log('self.labelData',self.labelData)
						for (var i = 0; i < self.mainData.sku.length; i++) {
						  /* if(self.mainData.sku[i].id==self.id){
						    self.skuData = self.$Utils.cloneForm(self.mainData.sku[i]);
						  }; */
										
						  self.choose_sku_item.push.apply(self.choose_sku_item,self.mainData.sku[i].sku_item);
						};
						if(self.mainData.sku.length>0){
							self.skuData = self.$Utils.cloneForm(self.mainData.sku[0]);
						};
						
						self.sku_item = self.skuData.sku_item;
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;height:auto"`);
						
						var array = self.$Utils.getStorageArray('footData');
						for (var i = 0; i < array.length; i++) {
							if (array[i].id == self.id) {
								var target = array[i]
							}
						};
						if (target) {
							target.count = target.count + 1
						} else {
							var target = self.mainData;
							target.count = 1;
							target.isSelect = true;
						}
						self.$Utils.setStorageArray('footData', target, 'id', 999);
					}
					self.getMessageData();
					uni.hideLoading();
				};
				self.$apis.productGet(postData, callback);
			},
			
			getMessageData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
					product_no: self.mainData.product_no,
					type: 1,
					user_type: 0
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.messageData.push.apply(self.messageData, res.info.data);
					}
					console.log('self.messageData', self.messageData)
					  
				};
				self.$apis.messageGet(postData, callback);
			},
			
			
			chooseSku(parentid,id){
				const self = this;
			    self.skuData = {};
				self.specsCurr = -1;
			    if(self.choose_sku_item.indexOf(id)==-1){
			      return;
			    };
			    self.choose_sku_item = [];
			    var sku = self.mainData.label[parentid];
			    for(var i=0;i<sku.children.length;i++){
			      if(self.sku_item.indexOf(sku.children[i].id)!=-1){
			        self.sku_item.splice(self.sku_item.indexOf(sku.children[i].id), 1);
			      };
			      self.choose_sku_item.push(sku.children[i].id);
			    };
			
			    
			    for (var i = 0; i < self.mainData.sku.length; i++) {
			      if(self.mainData.sku[i].sku_item.indexOf(parseInt(id))!=-1){
			        self.choose_sku_item.push.apply(self.choose_sku_item,self.mainData.sku[i].sku_item);  
			      };
			    };
			
			    for(var i=0;i<self.sku_item.length;i++){
			      if(self.choose_sku_item.indexOf(parseInt(self.sku_item[i]))==-1){
			        self.sku_item.splice(i, 1); 
			      };
			    };
			    self.sku_item.push(id);
			    for(var i=0;i<self.mainData.sku.length;i++){ 
			      if(JSON.stringify(self.mainData.sku[i].sku_item.sort())==JSON.stringify(self.sku_item.sort())){
			        //self.id = self.mainData.sku[i].id;
			        self.skuData = self.$Utils.cloneForm(self.mainData.sku[i]);
					self.specsCurr = i
			      };   
			    }; 
			},
			
			goBuy(){
				const self = this;
				if(self.mainData.type==4&&self.mainData.end_time<Date.parse(new Date())){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('商品已过购买时间', 'none');
					setTimeout(function() {
						self.Router.redirectTo({route:{path:'/pages/index/index'}})
					}, 1000);
					return
				};
				if(!self.mainData.sku[self.specsCurr]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('请选择规格或收货方式', 'none');
					return
				};
				if(self.mainData.type==2&&self.chooseWeek<0){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('请选择配送星期', 'none');
					return
				};
				uni.setStorageSync('canClick',false);
				self.orderList.push(
					{sku_id:self.mainData.sku[self.specsCurr].id,count:1,
					type:self.mainData.type,product:self.mainData,skuIndex:self.specsCurr},
				);
				uni.setStorageSync('payPro', self.orderList);
				if(self.$Utils.inArray(100,self.mainData.sku[self.specsCurr].sku_item)!=-1){
					console.log('y')
					self.Router.navigateTo({route:{path:'/pages/car-order/car-order?week='+self.chooseWeek+'&type=0'}})
				}else if(self.$Utils.inArray(101,self.mainData.sku[self.specsCurr].sku_item)!=-1){
					self.Router.navigateTo({route:{path:'/pages/car-order/car-order?week='+self.chooseWeek+'&type=1'}})
				}else{
					console.log('n')
					self.Router.navigateTo({route:{path:'/pages/car-order/car-order?week='+self.chooseWeek+'&type=0'}})
				};
				
				uni.setStorageSync('canClick',true);
			},
			
			addCar() {
				const self = this;
				if(!self.mainData.sku[self.specsCurr]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('请选择规格或收货方式', 'none');
					return
				};
				self.gg_show = false;
				var obj = self.mainData;
				if(self.$Utils.inArray(100,self.mainData.sku[self.specsCurr].sku_item)!=-1){
					self.mainData.transport_type = 0
				}else if(self.$Utils.inArray(101,self.mainData.sku[self.specsCurr].sku_item)!=-1){
					self.mainData.transport_type = 1
				}else{
					self.mainData.transport_type = 0
				};
				self.mainData.skuIndex = self.specsCurr;
				self.mainData.skuId = self.mainData.sku[self.specsCurr].id;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].skuId == self.mainData.sku[self.specsCurr].id) {
						var target = array[i]
					}
				}
				
				console.log(target)
				if (target) {
					target.count = target.count + 1
				} else {
					console.log(111)
					var target = self.mainData;
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入成功', 'none');
				self.$Utils.setStorageArray('cartData', target, 'skuId', 999);
			},
		}
	}
</script>

<style scoped>
.banner .swiper-box{width: 750rpx;height: 750rpx;}
.banner image{width: 750rpx;height: 750rpx;}

.cardBox .on{position: relative;color: #FF6740;}
.cardBox .on::before{content: '';width: 100rpx;height: 5rpx;background-color: #FF6740;position: absolute;bottom: 0;left: 50%;margin-left: -50rpx;}

.ms image{width: 100%;height: 400rpx;margin-top: 40rpx;}

.fh-icon{width: 42rpx;height: 33rpx;margin: auto;}
.btn{width: 280rpx;line-height: 100rpx;background-color: #333;}


.ggBox{min-height: 900rpx;}
.gg{width: 182rpx;}
.gg image{width: 182rpx;height: 182rpx;border-radius: 20rpx;position: absolute;top: -60rpx;}
.span{background-color: #f5f5f5;padding: 10rpx 20rpx;margin-right: 30rpx;margin-bottom: 20rpx;display: inline-block;}
.ggPart .on{background-color: #FDF7F5;color: #FF6740;border: 1px solid #FF6740;}
.ggBtn{line-height: 80rpx;background-color: #333;width: 345rpx;}
.ggBtn:nth-child(2){background-color: #FF6740;}
.ggPartBox{max-height: 600rpx;}
</style>
