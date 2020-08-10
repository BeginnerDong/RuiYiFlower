<template>
	<view class="color2">
		<view class="p-r pt-4">
			<image src="../../static/images/about-icon13.png" class="userBg"></image>
			
			<view class="p-r bg-white line-h text-center mx-3 radius10">
				<view class="colorR money">{{userInfoData.balance?userInfoData.balance:0}}</view>
				<view class="font-26 pb-5">可用余额</view>
			</view>
		</view>
		
		<view class="mx-3 px-2 py-3 bg1 mt-2">明细</view>
		<view class="px-2 mx-3 bg-white line-h">
			<view class="d-flex a-start j-sb bB-f5  py-3" v-for="(item,index) in mainData" :key="index">
				<view class="font-20 borderM radius Mcolor" v-if="item.count>0">充</view>
				<view class="flex-1 px-1">
					<view class="font-28 pb-2">{{item.trade_info}}</view>
					<view class="font-22 color9">{{item.create_time}}</view>
				</view>
				<view class="font-28 colorR">{{item.count}}</view>
			</view>

		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				
				userInfoData:{},
				searchItem:{
					thirdapp_id:2,
					type:2,
				},
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData','getUserInfoData'], self);
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
			
			getUserInfoData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0]
					}
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				if(isNew){
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
						
				};
				self.$apis.flowLogGet(postData, callback);
			},
		}
	};
</script>

<style>
.userBg{width: 750rpx;height: 180rpx;position: absolute;top: 0;}
.money{font-size: 70rpx;font-weight: 800;padding: 60rpx 0 34rpx;}

.bg1{background: #FDF7F5;}
</style>
