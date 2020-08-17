<template>
	<view>
		
		<view class="">
			<view class="left line-h h-100 font-26 color6 p-f top-0 bottom bg-f5">
				<view class="py-3 classLi" v-for="(item,index) in menuData" :key="item.id"
				 @click="changeLeft(index)" :class="leftCurr==index?'on':''" v-show="item.id == 56">{{item.title}}</view>
				<view class="py-3 classLi" @click="changeLeft(-1)" :class="leftCurr==-1?'on':''">包月鲜花</view>
				<view class="py-3 classLi" v-for="(item,index) in menuData" :key="item.id"
				 @click="changeLeft(index)" :class="leftCurr==index?'on':''" v-show="item.id != 56">{{item.title}}</view>
			</view>
			
			<view class="right h-100 bg-white flexY flex-column flex-1">
				<view class="p-3 pb-1 d-flex" v-for="(item,index) in mainData" :key="item.id" :data-id="item.id"
				@click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})">
					<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="radius10"></image>
					<view class="pl-2 d-flex flex-column j-sb flex-1">
						<view class="font-28 color2 avoidOverflow2 tit">{{item.title}}</view>
						<view class="d-flex j-sb">
							<view class="price font-28">{{item.price}}</view>
							<view class="font-22 color9">销量:{{item.sale_count}}</view>
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
			<view class="item on" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
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
		<view style="width: 100%;height: 5px;"></view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				leftCurr:-1,
				menuData:[],
				searchItem:{
					thirdapp_id:2,
					type:1,
				},
				mainData:[],
				isLoadAll:false,
				cartCount:0
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			if(options.index){
				self.index = options.index
			};
			self.$Utils.loadAll(['getMenuData'], self);
		},
		onReachBottom(){
			const self = this;
			console.log('onReachBottom');
			if(!self.isLoadAll){
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		onShow() {
			const self = this;
			self.cartCount = 0;
			self.cartData = self.$Utils.getStorageArray('cartData');
			for (var i = 0; i < self.cartData.length; i++) {
				 self.cartCount += self.cartData[i].count
			}
		},
		
		methods: {
			
			changeLeft(index){
				const self = this;
				if(self.leftCurr!=index){
					self.leftCurr = index;
					if(self.leftCurr==-2){
						self.searchItem.type = 1;
						delete self.searchItem.category_id
					}else if(self.leftCurr==-1){
						self.searchItem.type = 2
						delete self.searchItem.category_id
					}else{
						self.searchItem.type = 1;
						self.searchItem.category_id = self.menuData[self.leftCurr].id
					};
					self.isLoadAll = false;
					self.getMainData(true)
				}
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
				//postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.order = {
					listorder:'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}else{
						self.isLoadAll = true;
					};
					uni.setStorageSync('canClick', true);
					console.log('isLoadAll',self.isLoadAll)
					console.log('main',self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			
			getMenuData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
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
						self.menuData = res.info.data;
						if(self.index){
							self.changeLeft(self.index)
						}else{
							self.getMainData()
						}
					}
					self.$Utils.finishFunc('getMenuData');
				};
				self.$apis.labelGet(postData, callback);
			},
		}
	}
</script>

<style>
page{background-color: #fff;}

.left{width: 180rpx;padding-bottom: 100rpx;overflow-y: auto;}
.left .classLi{text-align: center;margin-bottom: 40rpx;}
.left .on{color: #FF6740;position: relative;}
.left .on::before{content: ''; height: 60rpx;width: 14rpx;border-radius: 7rpx;background-color: #FF6740;position: absolute;left: -7rpx;top: 14rpx;}

.right{padding-bottom: 120rpx;margin-left: 180rpx;}
.right image{width: 200rpx;height: 140rpx;}
.right .tt{width: 320rpx;}
</style>
