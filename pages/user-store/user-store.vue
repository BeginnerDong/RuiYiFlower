<template>
	<view class="font-26 color6 line-h">
		
		<view class="flex1 px-3 py-4 bB-f5 bg-white" v-for="(item,index) in mainData" :key="item.id">
			<view class="flex-1">
				<view><text class="font-28 color2 pr-3">{{item.info?item.info.name:''}}</text> {{item.info?item.info.phone:''}}</view>
				<view class="pt-3">{{item.info?item.info.address:''}}</view>
			</view>
			<image @click="setDefault(index)" :src="defaultNo!=''&&defaultNo == item.user_no?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'" class="shop-icon"></image>
		</view>	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				
				mainData:[],
				defaultNo:''
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
				postData.searchItem = {
					thirdapp_id:2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userInfoData = res.info.data[0]
						self.defaultNo = self.userInfoData.passage1
					};
					self.$Utils.finishFunc('getUserInfoData');	
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			setDefault(index) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				postData.data = {
					passage1:self.mainData[index].user_no
				};
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.defaultNo = self.mainData[index].user_no
						uni.setStorageSync('choosedShopData', self.mainData[index].info);
						console.log('choosedIndex', self.choosedIndex);
						uni.navigateBack({
							delta: 1
						})
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			
			
			getMainData(isNew) {
				const self = this;
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
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					user_type:1,
					thirdapp_id:2,
					behavior:1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
						
					};
					self.$Utils.finishFunc('getMainData');	
				};
				self.$apis.commonUserGet(postData, callback);
			},
		}
	}
</script>

<style>

</style>
