<template>
	<view>
		<!-- 搜索 -->
		<view class="flex1 pt-3 mx-3 p-r " style="z-index: 100;" 
		@click="Router.navigateTo({route:{path:'/pages/search/search'}})">
			<view class="d-flex radius30 py-2 w-100" style="background-color: rgba(255,255,255,0.5);">
				<image class="mx-2" src="../../static/images/search.png" style="width: 30rpx;height: 30rpx;" mode=""></image>
				<view class="color6 font-24">搜索您想要搜索的商品</view>
			</view>
		</view>
		
		<!-- banner -->
		<view class="banner radius20 overflow-h mx-3 mt-3">
			<view class="headBg p-a top-0 left-0 right-0"><image src="../../static/images/about-icon13.png" mode="widthFix"></image></view>
			<swiper class="swiper-box" indicator-dots="indicatorDots" :autoplay="autoplay" interval="3000" indicator-active-color="#FF6F48">
				<block>
					<swiper-item class="swiper-item"  v-for="(item,index) in sliderData.mainImg" :key="index">
						
						<image v-if="item.type=='image'" :src="item.url"
						 mode="widthFix" />
						<video style="height: 300rpx;width: 690rpx;" id="myVideo" loop  show-play-btn controls @click="ZhanTing"  objectFit="cover" v-if="item.type=='vedio'"
						 :src="item.url"></video>
					</swiper-item>
				</block>
			</swiper>
		</view>
		
		<!-- 金刚区 -->
		<view class="mx-3 d-flex j-sb a-end mt-3">
			<view class="d-flex flex-column a-center tt" v-for="(item,index) of menuData" :key="item.id" :data-index="index"
			@click="Router.navigateTo({route:{path:'/pages/classify/classify?index='+$event.currentTarget.dataset.index}})">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">{{item.title}}</view>
			</view>
			
			<view class="d-flex flex-column a-center tt" 
			@click="Router.navigateTo({route:{path:'/pages/user-collectCoupons/user-collectCoupons'}})">
				<image :src="img2Data.mainImg&&img2Data.mainImg[0]?img2Data.mainImg[0].url:''" class="icon"></image>
				<view class="font-24 color2 line-h pt-3">领券中心</view>
			</view>
		</view>
		<view class="mt-3 mx-3" @click="Router.navigateTo({route:{path:'/pages/article/article'}})">
			<image style="height: 160rpx;" :src="imgData.mainImg&&imgData.mainImg[0]?imgData.mainImg[0].url:''" mode="aspectFill"></image>
		</view>
		<!-- 热门专区 -->
		<view class="line-h font-32 color2 mt-3 mb-3 mx-3 Tit">热卖专区</view>
		<view class="line-h flexX">
			<view class="p-r ml-3 flex-shrink" v-for="(item,index) in hotData" :key="item.id" :data-id="item.id"
			 @click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="font-22 colorf sgin">销量:{{item.sale_count}}</view>
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="hotImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow hotTit">{{item.title}}</view>
				<view class="font-28 price">{{item.price}}</view>
			</view>
		</view>
		
		<!-- 新品推荐 -->
		<view class="line-h font-32 color2 mt-5 mb-3 mx-3 Tit">新品推荐</view>
		<view class="line-h flexX">
			<view class="p-r ml-3 flex-shrink" v-for="(item,index) in newData" :key="item.id" :data-id="item.id"
			 @click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="font-22 colorf sgin">销量:{{item.sale_count}}</view>
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="hotImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow hotTit">{{item.title}}</view>
				<view class="font-28 price">{{item.price}}</view>
			</view>
		</view>
		
		<!-- 包月鲜花 -->
		<view class="line-h font-32 color2 mt-5 mb-3 mx-3 Tit">限时抢购</view>
		<view class="line-h">
			<view class="p-r ml-3 pb-5" v-for="(item,index) in monthData" :key="item.id" :data-id="item.id"
			 @click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="yueImg"></image>
				<view class="font-30 color2 font-w pt-3 pb-2 avoidOverflow yueTit">{{item.title}}<span class="font-24 pl-2" style="color:#FF6F48">截止至：{{Utils.timeto(item.end_time,'ymd-hms')}}</span></view>
				<view class="font-28 price">{{item.price}}</view>
			</view>
		</view>
		<button class="p-f" open-type="contact" style="right: 2%;bottom: 20%;border-radius: 50%;overflow: hidden;">
			<image src="../../static/images/kefu-index.png" style="width: 80rpx;height: 80rpx;"></image>
		</button>
		
		
		<view :style="iPhoneX?'height: 170rpx;':'height: 130rpx'"></view>
		<!-- footer -->
		<view class="footer" :class="iPhoneX?'D':''">
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})" style="position: relative;">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
				<view style="width: 30rpx;height: 30rpx;line-height: 30rpx;border-radius: 50%;text-align: center;
				background-color: #FF6740;color: #fff;position: absolute;right: 24rpx;top: 4rpx;">{{cartCount}}</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar5.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	const app = getApp();
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				statusBar: app.globalData.statusBar,
				iPhoneX:false,
				is_show: false,
				menuData:[],
				sliderData:{},
				hotData:[],
				newData:[],
				monthData:[],
				cartCount:0,
				autoplay:true,
				imgData:{},
				img2Data:{}
			}
		},
		
		onLoad() {
			const self = this;
			if (uni.getStorageSync('isIphoneX')) {
				self.iPhoneX = true;
			}
			self.$Utils.loadAll(['getMenuData','getSliderData','getHotData','getNewData','getMonthData','getUserData','getImgData','getImg2Data'], self);
		},
		
		onShow() {
			const self = this;
			self.cartCount = 0;
			self.cartData = self.$Utils.getStorageArray('cartData');
			for (var i = 0; i < self.cartData.length; i++) {
				 self.cartCount += self.cartData[i].count
			}
		},
		
		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				return {
					title:"瑞意花木",
					path: '/pages/index/index', //点击分享的图片进到哪一个页面
					//imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
				}
			}else{
				return {
					title:"瑞意花木",
					path: '/pages/index/index', //点击分享的图片进到哪一个页面
				}
			}
		},
		
		onShareTimeline(){
			const self = this;
			return{
				title: '瑞意花木',
			}
		},
		
		methods: {
			
			getImg2Data() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'领劵中心'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.img2Data = res.info.data[0];
					};
					self.$Utils.finishFunc('getImg2Data');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getImgData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'menu_id',
						key: 'id',
						searchItem: {
							title: ['in', ['文章']],
						},
						condition: 'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.imgData = res.info.data[0];
					};
					console.log(self.mainData)
					self.$Utils.finishFunc('getImgData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			ZhanTing() {
				const self = this;
				self.autoplay = !self.autoplay
			},
			
			getUserData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				if(!wx.getStorageSync('user_info')||wx.getStorageSync('user_info').headImgUrl==''||!wx.getStorageSync('user_info').headImgUrl){
				  postData.refreshToken = true;
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0]
					};
					self.showAll = true;
					uni.setStorageSync('canClick', true);
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			getSliderData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'首页轮播'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.sliderData = res.info.data[0]
					}
					self.$Utils.finishFunc('getSliderData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			getHotData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:1,
					on_shelf:1,
					hot:1
				};
				/* postData.paginate = {
					count: 0,
					currentPage: 1,
					pagesize: 3,
					is_page: true,
				}; */
				postData.order = {
					create_time:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.hotData = res.info.data
					}
					self.$Utils.finishFunc('getHotData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getNewData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:1,
					on_shelf:1,
					new:1
				};
				postData.paginate = {
					count: 0,
					currentPage: 1,
					pagesize: 3,
					is_page: true,
				};
				postData.order = {
					sale_count:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.newData = res.info.data
					}
					self.$Utils.finishFunc('getNewData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getMonthData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:4,
					on_shelf:1,
					end_time:['>',Date.parse(new Date())]
				};
				/* postData.paginate = {
					count: 0,
					currentPage: 1,
					pagesize: 3,
					is_page: true,
				}; */
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.monthData = res.info.data
					}
					self.$Utils.finishFunc('getMonthData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getMenuData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.paginate = {
					count: 0,
					currentPage: 1,
					pagesize: 4,
					is_page: true,
				};
				postData.getBefore = {
					article: {
						tableName: 'Label',
						middleKey: 'parentid',
						key: 'id',
						searchItem: {
							title: ['in', ['鲜花商品']],
						},
						condition: 'in'
					}
				};
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.menuData = res.info.data
					}
					self.$Utils.finishFunc('getMenuData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			
			
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>
<style>
.headBg image{height: 180rpx;}
.banner .swiper-box{width: 690rpx;height: 300rpx;}

	button::after{
		border: none;
	}
.tt .icon{height: 112rpx!important;width: 112rpx!important;border-radius: 50%;}
.tt:nth-child(2) .icon{height: 102rpx;width: 122rpx;}
.tt:nth-child(3) .icon{height: 105rpx;width: 111rpx;}
.tt:nth-child(4) .icon{height: 129rpx;width: 109rpx;}
.tt:nth-child(5) .icon{height: 100rpx;width: 102rpx;}

.Tit{position: relative;text-indent: 18rpx;}
.Tit::before {content: '';background-color: #FF6740;height: 20rpx;width: 10rpx;position: absolute;top: 0;left: 0;}

.sgin{background-color: rgba(0,0,0,0.3);width: 120rpx;line-height: 40rpx;border-top-left-radius: 10rpx;border-bottom-right-radius: 10rpx;text-align: center;position: absolute;top: 0;left: 0;z-index: 2;}
.hotImg{width: 260rpx;height: 300rpx;border-radius: 10rpx;}
.hotTit{width: 260rpx;}
.newImg{width: 500rpx;height: 300rpx;border-radius: 10rpx;}
.newTit{width: 500rpx;}
.yueImg{width: 690rpx;height: 416rpx;border-radius: 10rpx;}
.yueTit{width: 690rpx;}
</style>
