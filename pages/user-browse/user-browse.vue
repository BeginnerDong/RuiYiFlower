<template>
	<view>

		<view class="font-28 color2 bg-white px-3 py-2 flex1 browse"  v-for="(item,index) of mainData" :key="item.id"
		:data-id="item.id"
		 @click="Router.navigateTo({route:{path:'/pages/goodsDetail/goodsDetail?id='+$event.currentTarget.dataset.id}})"
		>
			<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" class="broImg"></image>
			<view class="d-flex flex-column j-sb con">
				<view class="font-w flex-1 tit avoidOverflow2">{{item.title}}</view>
				<view class="flex1">
					<view class="price">{{item.price}}</view>
					<view class="font-22">销量:{{item.sale_count}}</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:[],
				idArray:[]
			}
		},

		onLoad() {
			const self = this;
			var array = self.$Utils.getStorageArray('footData');
			console.log('array', array)
			self.mainData = array.sort(this.compare("count",false));
			console.log('self.mainData', self.mainData)
			for (var i = 0; i < self.mainData.length; i++) {
				self.idArray.push(self.mainData[i].id)
			}
			self.getMainData()
		},

		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:1,
					on_shelf:1,
					id:['in',self.idArray]
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data
					}
					self.$Utils.finishFunc('getNewData');
				};
				self.$apis.productGet(postData, callback);
			},

			compare(property, desc) {
				return function(a, b) {
					var value1 = a[property];
					var value2 = b[property];
					if (desc == true) {
						// 升序排列
						return value1 - value2;
					} else {
						// 降序排列
						return value2 - value1;
					}
				}
			}

		}
	}
</script>

<style>
	.broImg {
		width: 200rpx;
		height: 140rpx;
	}

	.browse .con {
		width: 455rpx;
		height: 140rpx;
	}

	.browse .con .tit {
		width: 455rpx;
	}
</style>
