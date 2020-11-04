<template>
	<view class="container">
		<view class="flex align-center justify-center" style="width: 90rpx;height: 90rpx;"><text @click="back(e)" class="iconfont text-dark">&#xe607;</text></view>
		<view class="flex align-center justify-center" style="height: 350rpx;">
			<text style="font-size: 50rpx;" class="text-dark">{{ loginType === 'psw' ? '账号密码登录' : '手机验证码登录' }}</text>
		</view>
		<view class="px-3" v-if="loginType === 'psw'">
			<input type="text" v-model="form.username" class=" px-3 mb-4 font rounded border-bottom" placeholder="昵称/手机号/邮箱" style="height: 100rpx;" />
			<view class="border-bottom flex">
				<input type="password" v-model="form.password" class=" px-3 font rounded" placeholder="请输入密码" style="height: 100rpx;width: 65%;" />
				<text v-if="type === 'login'" class="text-light-muted p-2">忘记密码</text>
			</view>
			<input
				v-if="type != 'login'"
				type="password"
				v-model="form.repassword"
				class="px-3 mb-4 font rounded border-bottom mt-2"
				placeholder="请输入确认密码"
				style="height: 100rpx;"
			/>
		</view>
		<view class="px-3" v-else>
			<view class="border-bottom flex">
				<text class="font-weight-bold p-3">+86</text>
				<input type="text" v-model="form.username" class="px-3 font rounded" placeholder="手机号" style="height: 100rpx;" />
			</view>
			<view class="border-bottom flex mt-3">
				<input type="password" v-model="form.password" class=" px-3 font rounded" placeholder="请输入密码" style="height: 100rpx;width: 60%;" />
				<text v-if="type === 'login' && !send" class="text-light-muted p-2 border bg-hover-light rounded" style="height: 40rpx;" @click="sendCode">获取验证码</text>
				<text v-if="send" class="text-light-muted p-2 border bg-hover-light rounded" style="height: 40rpx;" @click="sendCode">还剩{{ sec }}s</text>
			</view>
			<input
				v-if="type != 'login'"
				type="password"
				v-model="form.repassword"
				class="px-3 mb-4 font rounded border-bottom"
				placeholder="请输入确认密码"
				style="height: 100rpx;"
			/>
		</view>
		<view class="p-3 flex align-center justify-center" @click="submit">
			<view class="rounded-circle bg-main p-3 flex align-center justify-center flex-1" hover-class="bg-main-hover">
				<text class="text-white font-md">{{ type === 'login' ? '登 录' : '注 册' }}</text>
			</view>
		</view>
		<view class="flex align-center justify-center">
			<text class="text-hover-dark font p-2" @click="changeLoginType">{{ loginType === 'psw' ? '验证码登录' : '账号密码登录登录' }}</text>
			<text class="text-hover-dark font p-2">|</text>
			<text class="text-hover-dark font p-2" @click="changeType">{{ type === 'login' ? '注册账号' : '去登录' }}</text>
		</view>
		<view class="flex align-center justify-center"><text class="text-light-muted p-2">————社交账号登录————</text></view>
		<view class="flex align-center justify-center">
			<image class="p-3" style="width: 100rpx;height: 100rpx;" src="../../static/login/qq.png"></image>
			<image class="p-3" style="width: 100rpx;height: 100rpx;" src="../../static/login/wechat.png"></image>
			<image class="p-3" style="width: 100rpx;height: 100rpx;" src="../../static/login/weibo.png"></image>
		</view>
		<view class="align-center justify-between text-light-muted" style="padding: 110rpx;">
			注册即代表您同意
			<text style="color: #0062CC;">《XXX社区协议》</text>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			type: 'login',
			loginType: 'psw',
			send: false,
			sec: 60,
			form: {
				username: '',
				password: '',
				repassword: ''
			}
		};
	},
	methods: {
		back(e) {
			uni.navigateBack({
				delta: 1
			});
		},
		changeType() {
			this.type = this.type === 'login' ? 'reg' : 'login';
		},
		changeLoginType() {
			this.loginType = this.loginType === 'psw' ? 'phone' : 'psw';
		},
		submit() {
			let msg = this.type === 'login' ? '登录' : '注册';
			console.log('111111111111111');
			console.log(this.type, this.form);
			console.log(this.$H);
			this.$H.post('/' + this.type, this.form).then(res => {
				uni.showToast({
					title: msg + '成功',
					icon: 'none'
				});
				if (this.type === 'reg') {
					this.changeType();
					this.form = {
						username: '',
						password: '',
						repassword: ''
					};
				} else {
					this.$store.dispatch('login', res);
					uni.navigateBack({
						delta: 1
					});
				}
			});
		},

		sendCode() {
			this.send = true;
			// 倒计时60s结束后 可再次发送验证码
			let promise = new Promise((resolve, reject) => {
				let setTimer = setInterval(() => {
					this.sec = this.sec - 1;
					if (this.sec <= 0) {
						this.send = false;
						resolve(setTimer);
					}
				}, 1000);
			});
			promise.then(setTimer => {
				clearInterval(setTimer);
			});
		}
	}
};
</script>

<style>
.container {
	width: 750rpx;
	height: 100vh;
	margin: 0;
	padding: 100rpx 0 0 0;
	background-size: cover;
	/* background-image: linear-gradient(to bottom, #BA7ACE 0%, #8745FF 100%); */
}
</style>
