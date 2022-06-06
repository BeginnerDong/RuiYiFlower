<template>
	<view>
		<view class="bg-white px-3 py-2 d-flex j-sb a-center " style="position: sticky;top: 0;">
			<view class="bg-f5 radius30 px-2 hs60 d-flex a-center flex-1 py-1">
				<image class="mr-1" src="../../static/images/search.png" mode="" style="width: 30rpx;height: 30rpx;"></image>
				<input class="font-24 flex-1" type="text" v-model="searchStr" placeholder="搜索您想要找的商品" />
			</view>
			<view class="font-32 Mcolor pl-2" @click="search">搜索</view>
		</view>
		
		<view class="px-3 w-100">
			
			<view class="py-5 mt-5" v-if="mainData.length<=0">
				<image src="../../static/images/nullProduxt.png" class="null mx-a" mode=""></image>
			</view>
			
			<view class="d-flex p-2 border-bottom bg-white radius10 mt-2" v-for="(item,index) in mainData" :key="item.id" :data-id="item.id"
			@click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})">
				<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="radius10 w200" mode="aspectFill"></image>
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
</template>

<script>
	export default {
		data() {
			return {
				Router: this.$Router,
				
				paginate:{
					count: 0,
					currentPage: 1,
					pagesize: 10,
					is_page: true,
				},
				searchItem:{
					thirdapp_id: 2,
					on_shelf:1,
					type:['in',[1,2,4]]
				},
				mainData:[],
				isLoadAll:false,
				
				searchStr:'',
				
				longitude:0,
				latitude:0,
			}
		},
		onLoad(options) {
			const self = this;
		},
		onReachBottom() {
			const self = this;
			if (!self.isLoadAll) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		methods: {
			
			search(){
				const self = this;
				if(!self.searchStr)return;
				self.searchItem.title = ['LIKE',['%'+self.searchStr+'%']];
				self.getMainData(true);
			},
			
			getMainData(isNew) {
				const self = this;
				const postData = {};
				if(isNew){
					self.paginate.currentPage = 1;
					self.mainData = [];
				}
				postData.searchItem = self.searchItem;
				postData.paginate = self.paginate;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}else{
						self.$Utils.showToast('未搜索到相关商品','none')
					};
					if(res.info.data.length<self.paginate.pagesize){
						self.isLoadAll = true;
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.productGet(postData, callback);
			},
			
		}
	}
</script>

<style scoped>
	.w200{width: 200rpx;height: 140rpx;}
	.tt{width: 320rpx;}
</style>
<style>
	
</style>
