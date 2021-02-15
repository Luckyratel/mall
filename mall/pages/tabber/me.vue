<template>
	<view class="container">
		<view class="header_box">
			<view class="header_fill_box"></view>
			<view class="header_content">
				<view class="header_left">
					<image></image>
					<text>小布</text>
				</view>
				<view class="header_right">
					<image></image>
					<image></image>
				</view>
			</view>
		</view>
		<view class="middle_box">
			<view class="middle_feature">
				<!-- <let-feature :customStyle="customStyle" titleText="我的订单" titleLabel="更多"></let-feature> -->
				<let-feature mode="swiper" swiperHeight="150rpx" :customStyle="customStyle" :titleHide="true"></let-feature>
			</view>
		</view>
	</view>
</template>

<script>
	import letFeature from '@/components/let-feature/let-feature.vue'
	export default{
		components:{
			letFeature
		},
		data(){
			return{
				customStyle: {
					'borderRadius': '10rpx',
					'background': '#FFFFFF',
					'paddingBottom': '0rpx'
				}
			}
		}
	}
</script>

<style lang="scss">
	.container{
		width: 100%;
		.header_box{
			height: 88rpx;
			width: 100%;
			position: relative;
			padding-top: var(--status-bar-height);
			background-color: $uni-title-color;
			.header_fill_box{
				height: 100%;
				width: 100%;
				z-index: -1;
			}
			.header_content{
				position: fixed;
				height: 88rpx;
				padding-top: var(--status-bar-height);
				background-color: $uni-title-color;
				width: 100%;
				top: 0rpx;
				left: 0rpx;
				z-index: 10;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.header_left{
					height: 100%;
					display: flex;
					align-items: center;
					margin-left: 30rpx;
					&>image{
						height: 50rpx;
						width: 50rpx;
						border-radius: 50%;
						background: #FFFFFF;
					}
					&>text{
						margin-left: 20rpx;
						color: #FFFFFF;
						font-size: 24rpx;
					}
				}
				.header_right{
					height: 100%;
					display: flex;
					align-items: center;
					margin-right: 30rpx;
					&>image{
						height: 50rpx;
						width: 50rpx;
						background-color: #FFFFFF;
					}
					&>image:nth-child(2){
						margin-left: 10rpx;
					}
				}
			}
			
		}
		.middle_box{
			width: 100%;
			margin-top: 20rpx;
			.middle_feature{
				width: calc(100% - 60rpx);
				margin-left: 30rpx;
			}
		}
	}
</style>
