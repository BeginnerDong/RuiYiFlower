<template>
	<view>
		<view class="font-28 color2 flex1 px-4 py-2 bg-white" v-for="item in mainData" :key="item.id">
			<image :src="item.relationUser&&item.relationUser[0]&&item.relationUser[0].headImgUrl!=''?item.relationUser[0].headImgUrl:'../../static/images/head.png'" class="shareImg"></image>
			<view class="flex-1 pl-2">{{item.relationUser&&item.relationUser[0]&&item.relationUser[0].nickname!=''?item.relationUser[0].nickname:'用户'+item.relationUser[0].user_no}}</view>
			<view class="font-26 color6">订单数：{{item.orderNum.num}}</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				searchItem:{
					thirdapp_id:2,
					//level:1
				},
				mainData:[],
				Router:this.$Router,
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			
			self.$Utils.loadAll(['getMainData'], self);
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
			
			getMainData(isNew) {
				const self = this;
				console.log('isNew',isNew)
				if (isNew) {
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
				postData.searchItem.parent_no = uni.getStorageSync('user_info').user_no;
				postData.sTokenAfter = 'parent_no';
				postData.getAfter = {
					relationUser:{
						tableName:'User',
						middleKey:'child_no',
						key:'user_no',
						searchItem:{
							status:1
						},
						condition:'in',
					},
					orderNum:{
						tableName:'Order',
						middleKey:'child_no',
						key:'user_no',
						searchItem:{
							status:1,
							pay_status:1
						},
						condition:'in',
						compute: {
							num: [
								'count',
								'count',
								{
									status:1,
									pay_status:1
								}
							],
						},
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					};
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.distriGet(postData, callback);
			},
			
		}
	}
</script>

<style>
.shareImg{width: 80rpx;height: 80rpx;}
</style>
