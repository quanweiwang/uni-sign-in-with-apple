<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<!-- 苹果登录 -->
		<view class="sign-in-with-apple" v-if="system >= 13 && platform=='ios'" @click="appleLogin">sign in with apple</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				system: '',	// 系统版本
				platform: '',	// 平台
			}
		},
		onLoad() {
			// 先判断 系统版本
			uni.getSystemInfo({
				success: (res) => {
					this.system = res.system
					this.platform = res.platform
				},fail: (err) => {
					
				},complete: () => {
					
				}
			})
			
		},
		methods: {
			// 苹果登录
			appleLogin() {
				// 判断是 iOS13版本
				uni.login({
					provider: 'apple',
					success: (loginRes) => {
						uni.getUserInfo({
							provider: 'apple',
							success: (userInfoRes) => {
								console.log(userInfoRes)
							},
							fail: (err) => {
								console.log(err)
							}
						})
					},
					fail: (err) => {
						console.log(err)
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	
	.sign-in-with-apple {
		margin-top: 20upx;
		background-color: #000000;
		width: 400upx;
		height: 80upx;
		color: #FFFFFF;
		text-align: center;
		line-height: 80upx;
		border-radius: 20upx;
	}
	
</style>
