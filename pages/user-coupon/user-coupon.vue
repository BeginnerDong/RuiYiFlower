<template>
	<view>
		
		<view class="font-28 color2 d-flex shadow list">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">未使用</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">已使用</view>
		</view>
		
		<view class="pt-3 px-3 line-h">
			<view class="d-flex flex-wrap">
				<view class="coupon-item p-r mt-2" v-for="(item,index) in mainData" :key="index">
					<image src="../../static/images/vip-icon5.png" class="vipBg2"></image>
					<view class="p-a colorR top-0 left-0 right-0 text-center">
						<view class="vipPrice pt-4 pb-1">{{item.value}}</view>
						<view class="font-18">满{{item.condition}}元使用</view>
						<view class="font-w pt-5 font-24">{{item.use_step==1?'未使用':'已使用'}}</view>
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
				liCurr:0,
				searchItem:{
					thirdapp_id: 2,
					use_step:1,
				},
				mainData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			changeLi(i){
				const self = this;
				if(self.liCurr!=i){
					self.liCurr = i;
					if(self.liCurr==0){
						self.searchItem.use_step=1
					}else{
						self.searchItem.use_step=2
					};
					self.getMainData(true)
				}
			},
			
			
			getMainData(isNew) {
				const self = this;
				var now =  (new Date()).getTime();
				if (isNew) {
					self.mainData = [];
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = self.$Utils.cloneForm(self.searchItem)
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userCouponGet(postData, callback);
			},
		}
	}
</script>

<style>
page{background-color: #fff;}
.li{width: 50%;}
.coupon-item{margin-right: 27rpx;}
.coupon-item:nth-child(3n){margin-right: 0;}
</style>
