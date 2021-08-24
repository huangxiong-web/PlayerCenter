<template>
	
	<view class="me">
		<image src="../../static/images/bg.jpg" mode=""></image>
		<view class="logo">
			<image src="/static/icons/logo.png" mode=""></image>
		</view>
			<view class="login">
				<image src="../../static/images/user.png" mode=""></image>
				<input type="text" value="" placeholder="用户名/手机号"/>
			</view>
			<view class="login-pwd">
				<image src="../../static/images/mima.png" mode=""></image>
				<input :type="pwd_type" value="" placeholder="密码"/>
				<image :src="pwd_icon" @click="pwd_visible=!pwd_visible"  mode=""></image>
			</view>
			<view class="btn-login" hover-class="active">
				登录
			</view>
			<view class="accout-area">
				<view>忘记密码?</view>
				<view>立即注册</view>
			</view>
			<view class="bottom">
				<view>
					<view class="line"></view>
					<view>第三方直接登录</view>
					<view class="line"></view>
				</view>
				<view>
					<image src="../../static/images/QQ.png" mode=""></image>
					<image src="../../static/images/weixin.png" mode=""></image>
					<image src="../../static/images/weibo.png" mode=""></image>
				</view>
			</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pwd_visible:false
			};
		},
		computed:{
			pwd_type(){
				return this.pwd_visible?'text':'password'
			},
			pwd_icon(){
				return this.pwd_visible?'/static/images/eye.png':'/static/images/eye-close.png'
			}
		}
	}
</script>

<style lang="scss">
	.active{
		opacity: 0.6;
	}
.me{
	// padding: 80rpx;
	width: 100%;
	height: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;
	
	>image{
		position: fixed;
		top: 0;
		left: 0;
		z-index: -1;
		width: 100%;
		height: 100%;
		// opacity: 0.8;
		filter: blur(6px);
	}
	}
	
	.logo{
		
		>image{
			width: 420rpx;
			height: 102rpx;
			border-radius: 8rpx;
			background-color: white;
			margin-top: 200rpx;
			
		}
		}
	.login{
		margin-top: 110rpx;
		height: 70rpx;
		width: 500rpx;
		border-radius: 6rpx;
		
		display: flex;
		align-items: center;
		background-color: white;
		>image{
			padding: 10rpx;
			width: 40rpx;
			height: 40rpx;
			}
		}
	.login-pwd{
		margin-top: 20rpx;
		height: 70rpx;
		width: 500rpx;
		border-radius: 6rpx;
		
		display: flex;
		align-items: center;
		background-color: white;
		>image{
			padding: 10rpx;
			width: 40rpx;
			height: 40rpx;
			}
		>input{
			flex:1;
			
		}
	}
	.btn-login{
		margin-top: 30rpx;
		height: 70rpx;
		width: 500rpx;
		border-radius: 6rpx;
		background-color: #ffa508;
		text-align: center;
		line-height: 70rpx;
		color: white;
	}		
	.accout-area{
		width: 500rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		color:#7a7e81;
		>view{
			padding: 10rpx;
			text-decoration: underline;
		}
	}
	.bottom{
		margin-top: 200rpx;
		color: white;
		view:first-child{
			display: flex;
			align-items: center;
			justify-content: center;
			>view:nth-child(2){
				padding: 0 15rpx;
			}
			.line{
				height: 1px;
				background-color: white;
				width: 175rpx;
				}
			}
		view:last-child{
			margin: 0 auto;
			// margin-top: 10rpx;
			display: flex;
			width: 500rpx;
			justify-content: space-between;
			align-items: center;
			>image{
				padding: 30rpx 20rpx 0 20rpx;
				width: 70rpx;
				height: 70rpx;
			}
		}
	}
	

</style>
