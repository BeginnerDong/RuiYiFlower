<template>
	<view v-if="showAll">
		<view class="p-r">
			<image src="../../static/images/about-icon13.png" class="userBg"></image>
			<view class="p-r p-3 color2 font-24 line-h d-flex" v-if="userData.nickname">
				
				<image :src="userData.headImgUrl?userData.headImgUrl:''" class="userImg"></image>
				<view class="font-30 colorf pt-1 pl-2">
					<view class="pb-2">{{userData.nickname?userData.nickname:''}}</view>
					<view class="font-22 p-r" v-if="userData.behavior==1">
						<image src="../../static/images/about-icon.png" class="userVip"></image>
						<view class="p-r line-h-md pl-4">会员</view>
					</view>
				</view>
			</view>
			<view class="p-r p-3 color2 font-24 line-h d-flex" style="padding-top: 60rpx;padding-bottom: 60rpx;justify-content: center;" v-if="userData.nickname==''">
				<button style="padding: 0 10px;font-size: 13px;background-color: #fff;color: #FF6F48;height: 25px;line-height: 25px;"
				v-if="userData.nickname==''" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">点击获取头像</button>
			</view>
			<view class="bg-black mx-4  p-3 pb-5 p-r colorG font-32 d-flex j-sb a-center radius20-T yy"  @click="Router.navigateTo({route:{path:'/pages/user-surplus/user-surplus'}})">
				<view class="d-flex a-center" v-if="userData.behavior==1">{{userData.info?userData.info.balance:0}}<text class="font-22 pl-1">(余额)</text></view>
				<view class="font-24 d-flex a-center" v-if="userData.behavior==1">查看<image src="../../static/images/about-icon1.png" class="R-icon"></image></view>
				<view class="d-flex a-center" style="font-size: 14px;" v-if="userData.behavior==0">成为会员享更多优惠~</view>
			</view>
			<!-- <button v-if="userData.nickname==''" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">点击登录</button> -->
		</view>
		
		<view class="p-r">
			<image src="../../static/images/vip-img0.png" class="bgImg"></image>
			
			<view class="p-r color2">
				<view class="px-3 bB-f5 pb-4">
					<view class="font-30 pb-3 pt-4 font-w">我的订单</view>
					<view class="d-flex j-sb a-center order">
						<view class="item font-24 radius10 d-flex j-sb a-center px-3" @click="Router.navigateTo({route:{path:'/pages/user-order/user-order?id=0'}})">
							<image src="../../static/images/about-icon2.png" mode=""></image>
							<view>门店订单</view>
						</view>
						<view class="item font-24 radius10 d-flex j-sb a-center px-3" @click="Router.navigateTo({route:{path:'/pages/user-order/user-order?id=1'}})">
							<image src="../../static/images/about-icon3.png" mode=""></image>
							<view>送货订单</view>
						</view>
						<view class="item font-24 radius10 d-flex j-sb a-center px-3" @click="Router.navigateTo({route:{path:'/pages/user-order/user-order?id=2'}})">
							<image src="../../static/images/about-icon4.png" mode=""></image>
							<view>包月订单</view>
						</view>
					</view>
				</view>
				
				<view class="px-3 bB-f5 pb-4">
					<view class="font-30 pb-3 pt-4 font-w">常用工具</view>
					<view class="d-flex j-sb a-end">
						<view class="font-24 d-flex a-center flex-column" @click="Router.navigateTo({route:{path:'/pages/user-coupon/user-coupon'}})">
							<image src="../../static/images/about-icon5.png" class="user-icon"></image>
							<view>优惠券</view>
						</view>
						<view class="font-24 d-flex a-center flex-column" @click="Router.navigateTo({route:{path:'/pages/user-address/user-address'}})">
							<image src="../../static/images/about-icon6.png" class="user-icon1"></image>
							<view>收货地址</view>
						</view>
						<view class="font-24 d-flex a-center flex-column" @click="Router.navigateTo({route:{path:'/pages/user-share/user-share'}})">
							<image src="../../static/images/about-icon7.png" class="user-icon2"></image>
							<view>我的分享</view>
						</view>
						<view class="font-24 d-flex a-center flex-column" @click="Router.navigateTo({route:{path:'/pages/user-browse/user-browse'}})">
							<image src="../../static/images/about-icon8.png" class="user-icon3"></image>
							<view>浏览记录</view>
						</view>
						<view class="font-24 d-flex a-center flex-column" @click="Router.navigateTo({route:{path:'/pages/user-aboutUs/user-aboutUs'}})">
							<image src="../../static/images/about-icon9.png" class="user-icon4"></image>
							<view>联系我们</view>
						</view>
					</view>
				</view>
				
				<view class="px-3 pb-4">
					<view class="font-30 pb-3 pt-4 font-w">第三方入口</view>
					<view class="d-flex a-end">
						<view class="font-24 d-flex a-center flex-column mr-5" @click="login('staff')">
							<image src="../../static/images/about-icon10.png" class="user-icon5"></image>
							<view>自提入口</view>
						</view>
						<view class="font-24 d-flex a-center flex-column ml-1" @click="login('rider')">
							<image src="../../static/images/about-icon11.png" class="user-icon6"></image>
							<view>配送员入口</view>
						</view>
					</view>
				</view>
				
			</view>
		
		</view>
		
		
		
		
		
		
		<!-- footer -->
		<view class="footer">
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
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar5-a.png" mode=""></image>
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
				showAll:false,
				userData:{},
				Utils:this.$Utils
			}
		},
		
		onLoad() {
			const self = this;
			if(uni.getStorageSync('user_token')){
				self.$Utils.loadAll(['getUserData'], self);
			}else{
				self.showAll = true
			}
		},
		
		methods: {
			
			login(type){
				const self = this;
				if(type=='staff'){
					if(uni.getStorageSync('staffToken')){
						self.Router.navigateTo({route:{path:'/pages/user-zitiEntrance/user-zitiEntrance'}})
					}else{
						self.Router.navigateTo({route:{path:'/pages/login/login?type=staff'}})
					}
				}else if(type=='rider'){
					if(uni.getStorageSync('riderToken')){
						self.Router.navigateTo({route:{path:'/pages/user-Distributor/user-Distributor'}})
					}else{
						self.Router.navigateTo({route:{path:'/pages/login/login?type=rider'}})
					}
				}
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const callback = (user, res) => {
					console.log(res)
					self.getUserData();
				};
				self.$Utils.getAuthSetting(callback);
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
			
		}
	}
</script>

<style>
.colorG{color: #DEBF92;}
.userBg{width: 750rpx;height: 382rpx;position: absolute;}
.userImg{width: 90rpx;height: 90rpx;border-radius: 50%;overflow: hidden;}
.userVip{width: 100rpx;height: 32rpx;position: absolute;}
.yy{line-height: 32rpx;}

.bgImg{width: 750rpx;height: 980rpx;position: absolute;top: -40rpx;}
.order .item{width: 210rpx;height: 80rpx;background-color: #EFF4FF;box-sizing: border-box;}
.order .item:nth-child(2){background-color: #E8FFF7;}
.order .item:nth-child(3){background-color: #FFF7E9;}
.order .item image{width: 38rpx;height: 38rpx;}
.order .item:nth-child(2) image{width: 44rpx;height: 34rpx;}
.order .item:nth-child(3) image{width: 34rpx;height: 40rpx;}

.user-icon{width: 46rpx;height: 40rpx;margin-bottom: 20rpx;}
.user-icon1{width: 41rpx;height: 48rpx;margin-bottom: 20rpx;}
.user-icon2{width: 42rpx;height: 42rpx;margin-bottom: 20rpx;}
.user-icon3{width: 41rpx;height: 48rpx;margin-bottom: 20rpx;}
.user-icon4{width: 46rpx;height: 40rpx;margin-bottom: 20rpx;}
.user-icon5{width: 46rpx;height: 44rpx;margin-bottom: 20rpx;}
.user-icon6{width: 40rpx;height: 52rpx;margin-bottom: 20rpx;}
</style>
