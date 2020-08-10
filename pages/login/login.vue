<template>
	<view class="line-h">
		<view class="font-50 head">账号登录</view>
		
		<view class="login font-26 pb-1">
			<input type="text" v-model="submitData.login_name" placeholder="请输入手机号" />
			<input type="password" v-model="submitData.password" placeholder="请输入密码" />
		</view>
		
		<view class="Btn600" @click="submit">确定</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				submitData:{
					login_name:'',
					password:''
				},
				showAll:true,
				type:''
			}
		},
		onLoad(options) {
			const self = this;
			uni.hideLoading();
			self.type = options.type
			// self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
		
			submit() {
				const self = this;
				const postData = {
					login_name: self.submitData.login_name,
					password:self.submitData.password
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					const callback = (res) => {
						if (res.solely_code == 100000) {
							if(self.type=='staff'){
								uni.setStorageSync('staffToken', res.token);
								uni.setStorageSync('staffInfo', res.info);
								setTimeout(function() {
									self.Router.redirectTo({route:{path:'/pages/user-zitiEntrance/user-zitiEntrance'}})
								}, 1000);
							}else{
								uni.setStorageSync('riderToken', res.token);
								uni.setStorageSync('riderInfo', res.info);
								setTimeout(function() {
									self.Router.redirectTo({route:{path:'/pages/user-Distributor/user-Distributor'}})
								}, 1000);
							}
						} else {
							self.$Utils.showToast(res.msg,'none')
						}
					}
					if(self.type=='staff'){
						self.$apis.staffLogin(postData, callback);
					}else{
						self.$apis.riderLogin(postData, callback);
					}
				} else {
					self.$Utils.showToast('请补全登录信息', 'none')
				};
			},
		}
	};
</script>


<style>
page{background-color: #fff!important;}
.head{padding: 100rpx 0 120rpx 76rpx;}

.login input{padding: 40rpx 0 30rpx;border-bottom: 1px solid #f5f5f5;width: 600rpx;margin: auto;}
.login input::-webkit-input-placeholder{color: #999;}

.Btn600{background-color: #FF6740;width: 600rpx;height: 80rpx;line-height: 80rpx;color: #fff;font-size: 30rpx;text-align: center;border-radius: 40rpx;margin:  50rpx auto;}
</style>
