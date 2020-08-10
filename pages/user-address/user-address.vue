<template>
	<view class="line-h">
		
		<view class="font-28 color6 mb-2" v-for="(item,index) in mainData" :key="index">
			<view class="bB-f5 py-3 px-3">
				<view class="pb-3" @click="choose(index)"><text class="color2 pr-3">{{item.name}}</text>{{item.phone}}</view>
				<view @click="choose(index)">{{item.city+item.detail}}</view>
			</view>
			<view class="py-3 flex1 px-3">
				<view class="flex1" :data-id="item.id" @click="updateAddress($event.currentTarget.dataset.id)">
					<image :src="item.isdefault==1?'../../static/images/shopping-icon.png':'../../static/images/shopping-icon1.png'"class="shop-icon"></image>
					<!-- <image src="../../static/images/shopping-icon1.png" class="shop-icon"></image> -->
					<view class="pl-1">默认地址</view>
				</view>
				<view class="flex1">
					<view class="flex1" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/user-addAddress/user-addAddress?id='+$event.currentTarget.dataset.id}})">
						<image src="../../static/images/addressl-icon.png" class="add-icon"></image>
						<view>编辑</view>
					</view>
					<view class="flex1 ml-5" :data-id="item.id" @click="deleteAddress($event.currentTarget.dataset.id)">
						<image src="../../static/images/addressl-icon1.png" class="add-icon"></image>
						<view>删除</view>
					</view>
				</view>
			</view>
			<view class="f5-2"></view>
		</view>
		
		
		
		<view style="height: 120rpx;"></view>
		<view class="flex0 py-3 bT-f5 p-f bottom-0 left-0 right-0 addBot" @click="Router.navigateTo({route:{path:'/pages/user-addAddress/user-addAddress'}})">
			<image src="../../static/images/addressl-icon2.png" class="add-icon"></image>
			<view>新增地址</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {

		data() {
			return {
				mainData: [],
				Router: this.$Router,
				choosedIndex: -1
			}
		},

		onShow(options) {
			const self = this;
			self.mainData = [];
			var res = self.$Token.getProjectToken(function() {
				self.$Utils.loadAll(['getMainData'], self)
			});
			if (res) {
				self.$Utils.loadAll(['getMainData'], self)
			};
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

			choose(index) {
				const self = this;
				self.choosedIndex = index;
				uni.setStorageSync('choosedAddressData', self.mainData[index]);
				console.log('choosedIndex', self.choosedIndex);
				uni.navigateBack({
					delta: 1
				})
			},

			getMainData() {
				const self = this;

				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
				postData.tokenFuncName = 'getProjectToken';
				postData.order = {
					isdefault:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					} else {
						self.$Utils.showToast('没有更多了', 'none');
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.addressGet(postData, callback);
			},





			deleteAddress(id) {
				const self = this;
				uni.showModal({
					title: '提示',
					content: '确认是否删除这个地址',
					success: function(res) {
						if (res.confirm) {
							const postData = {};
							postData.searchItem = {};
							postData.searchItem.id = id;
							postData.tokenFuncName = 'getProjectToken';
							const callback = (res) => {
								if (res) {
									self.mainData = [];
									self.getMainData();
								}
							};
							self.$apis.addressDelete(postData, callback)
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});
			},


			updateAddress(id) {
				const self = this;
				const postData = {};

				postData.tokenFuncName = 'getProjectToken';

				postData.searchItem = {};
				postData.searchItem.id = id;
				postData.data = {
					isdefault: 1
				}
				const callback = (res) => {
					if (res) {
						self.mainData = [];
						self.getMainData();
					}
				};
				self.$apis.addressUpdate(postData, callback);
			},

		}
	}
</script>
<style>
	page{background: #fff;}
.add-icon{width: 26rpx;height: 26rpx;margin-right: 10rpx;}
.addBot{height: 100rpx;}
</style>