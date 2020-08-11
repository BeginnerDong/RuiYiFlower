<template>
	<view v-if="showAll">
		
		<view class="vipHead pt-3 px-3 p-r bg-black">
			
			<!-- 会员 -->
			<view class="p-r yesVip" v-if="userData.behavior==1">
				<image src="../../static/images/vip-icon7.png" ></image>
				<view class="p-aXY p-4 color2 font-24 line-h d-flex">
					<image style="overflow: hidden;border-radius:50%;" :src="userData.headImgUrl?userData.headImgUrl:''" class="vipImg"></image>
					<view class="font-30 color2 font-w pt-1 pl-2">
						<view>{{userData.nickname?userData.nickname:''}}</view>
						<view class="font-22 color2f mt-2 d-flex colorf vipSpan">
							<image src="../../static/images/vip-icon.png" class="vipIcon2"></image>
							<view>会员</view>
						</view>
					</view>
				</view>
			</view>
			
			<button class="lq font-26 radiusR-1" style="text-align: inherit;" v-if="userData.behavior!=1" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">领取会员</button>
			<!-- 非会员 -->
			<view class="p-r noVip" v-if="userData.behavior!=1">
				<image src="../../static/images/vip-icon7.png" ></image>
				<view class="p-aXY py-3 px-4 color2 font-24 line-h w-70">
					<view class="pb-5"><text class="font-40 font-w">会员VIP</text> 专享会员权益</view>
					<view>领取会员享受更多优惠</view>
				</view>
			</view>
			
		</view>
		
		<view class="p-r vipBox">
			<image src="../../static/images/vip-img0.png" class="vipBg"></image>
			
			<view class="line-h color2 px-3 p-r">
				<view class="font-32 py-4 font-w">会员权益</view>
				<view class="font-26 d-flex j-sb">
					<view class="d-flex flex-column a-center"
					@click="Router.navigateTo({route:{path:'/pages/VIP-recharge/VIP-recharge'}})">
						<image src="../../static/images/vip-icon1.png" class="vipIcon"></image>
						<view class="pt-3">专享充值</view>
					</view>
					<view class="d-flex flex-column a-center"
					@click="Router.navigateTo({route:{path:'/pages/user-collectCoupons/user-collectCoupons'}})">
						<image src="../../static/images/vip-icon2.png" class="vipIcon"></image>
						<view class="pt-3">领取优惠券</view>
					</view>
					<view class="d-flex flex-column a-center" @click="zxShow(1)">
						<image src="../../static/images/vip-icon3.png" class="vipIcon"></image>
						<view class="pt-3">专享服务</view>
					</view>
					<view class="d-flex flex-column a-center" @click="zxShow(2)">
						<image src="../../static/images/vip-icon4.png" class="vipIcon"></image>
						<view class="pt-3">专享福利</view>
					</view>
				</view>
				
				<!-- 会员展示 -->
				<view class="pt-3"  v-if="userData.behavior==1">
					<view class="font-32 py-4 font-w">优惠券专区</view>
					<view class="d-flex flex-wrap">
						<view class="p-r coupon-item" v-for="(item,index) in mainData" :key="index" v-if="index<3">
							<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
							<view class="p-a colorR top-0 left-0 right-0 text-center">
								<view class="vipPrice pt-4 pb-1">{{item.value}}</view>
								<view class="font-18">满{{item.condition}}元使用</view>
								<view class="font-w pt-5 font-24" @click="submitCoupon(index)" v-if="item.hasPick&&item.hasPick.length==0">立即领券</view>
								<view class="font-w pt-5 font-24" v-else>已领取</view>
							</view>
						</view>

					</view>
				</view>
				
			</view>
			
				
			
			<view class="btn690 p-a"  v-if="userData.behavior==1" @click="Router.navigateTo({route:{path:'/pages/VIP-recharge/VIP-recharge'}})">充值</view>
		</view>
		
		
		<view class="lq-exec p-fXY m-a radius10 text-center" v-show="yes_show">
			<view class="font-32 colorf">领取成功</view>
			<image src="../../static/images/vip-icon8.png" class="x-icon" @click="yesShow"></image>
		</view>
		
		<view class="bg-mask" style="padding-bottom: 100rpx;" v-show="zx_show!=0">
			<view class="mask bg-white radius20 p-aXY mx-a overflow-h flex5">
				<view class="py-3 text-center font-32 font-w bB-f5 w-100">{{zx_show==1?'专享服务':'专享福利'}}</view>
				<view class="flex-1 p-3 w-100">
					{{zx_show==1?'服务内容':'专享福利内容'}}
				</view>
				<view class="colorf font-30 Mgb py-3 text-center w-100" @click="zxShow(0)">确定</view>
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
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/VIP/VIP'}})">
				<image src="../../static/images/nabar3-a.png" mode=""></image>
				<view>会员</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})">
				<image src="../../static/images/nabar4.png" mode=""></image>
				<view>购物车</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar5.png" mode=""></image>
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
				Utils:this.$Utils,
				mainData:[],
				zx_show:0
			}
		},
		
		onLoad() {
			const self = this;
			if(uni.getStorageSync('user_token')){
				const callback = (res) => {
					
					self.$Utils.loadAll(['getMainData'], self);
				};
				self.$Token.getProjectToken(callback, {
					refreshToken: true,
				})	
			}else{
				self.showAll = true
			}
		},
		
		methods: {
			
			zxShow(i){
				const self = this;
				self.zx_show = i
			},
			
			submitCoupon(index){
				const self = this;
				self.orderList = [
					{coupon_id:self.mainData[index].id,count:1,type:self.mainData[index].type}
				];
				self.couponAdd()
			},
			
			couponAdd() {
				const self = this;
				var now =  (new Date()).getTime();
				const postData = {
					
					tokenFuncName: 'getProjectToken',
					
				};
				postData.couponList = self.$Utils.cloneForm(self.orderList);
				postData.pay = {
					score: 0
				};
				console.log('postData', postData)
				const callback = (res) => {
					if (res && res.solely_code == 100000) {
						self.$Utils.showToast('领取成功', 'none')
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						self.$Utils.showToast(res.msg, 'none')
					}
				};
				self.$apis.couponAdd(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const callback = (user, res) => {
					console.log(res)
					self.userUpdate();
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			userUpdate() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					behavior:1
				};
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.solely_code==100000) {
						self.$Utils.showToast('领取成功','none');
						setTimeout(function() {
							self.getUserData()
						}, 1000);	
					};
					uni.setStorageSync('canClick', true);
				};
				self.$apis.userUpdate(postData, callback);
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
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
				};
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
				};
				postData.getAfter = {
					hasPick:{
						token:uni.getStorageSync('user_token'),
						tableName:'UserCoupon',
						middleKey:'coupon_no',
						key:'coupon_no',
						searchItem:{
							status:1,
						},
						condition:'='
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.getUserData()
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.couponGet(postData, callback);
			},	
			
		}
	}
</script>

<style scoped>
page{background: #fff;}
.vipHead .noVip{width: 630rpx;height: 180rpx;}
.lq{background: #FDDFD2;width: 100rpx;height: 160rpx;position: absolute;bottom: 0;right: 30rpx;writing-mode: vertical-rl;line-height: 70rpx;color: #9C7032;padding-top: 30rpx;}
.yesVip{width: 690rpx;height: 180rpx;}
.vipImg{width: 90rpx;height: 90rpx;}
.vipIcon2{width: 32rpx;height: 32rpx;}
.vipSpan{line-height: 32rpx;background-color: #DEB883;border-radius: 16rpx;}
.vipSpan view{background-color: #DEB883;border-radius: 16rpx;text-indent: 10rpx;padding-right: 10rpx;}

.mask{width: 80%;height: 70%;top: 10%;}

.vipBox{height: 993rpx;}
.vipBg{width: 750rpx;height: 993rpx;position: absolute;top: -30rpx;}
.vipIcon{width: 90rpx;height: 90rpx;}
.btn690{bottom: 150rpx;}


.lq-exec{width: 400rpx;height: 160rpx;line-height: 160rpx;background-color: rgba(0,0,0,0.5);z-index: 100;}
.x-icon{position: absolute;right: 0;top: 0;margin: 20rpx;}
.coupon-item{margin-right: 27rpx;}
.coupon-item:nth-child(3n){margin-right: 0;}
</style>
