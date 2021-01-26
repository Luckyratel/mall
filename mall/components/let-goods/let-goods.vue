<template>
	<view class="let_goods_box">
		<view class="goods_img">
			<image></image>
		</view>
		<view class="goods_name"> <text>示例商品示例商品示例商品示例商品示例商品</text> </view>
		<view class="goods_price_box">
			<view class="sale_price">
				<text style="font-size: 20rpx;">￥</text>
				<text>1000</text>
			</view>
			<view class="market_price"><text>￥700</text> </view>
		</view>
		<view class="goods_label">
			<view class="common_label"> <text>限时特价</text> </view>
			<view class="common_label"> <text>积分双倍</text> </view>
		</view>
		
	</view>
</template>

<script>
</script>

<style lang="scss">
	.let_goods_box{
		width: 340rpx;
		display: flex;
		align-items: center;
		flex-direction: column;
		box-sizing: border-box;
		padding: 10rpx;
		border-radius: 6rpx;
		.goods_img{
			height: 320rpx;
			width: 320rpx;
			&>image{
				height: 100%;
				width: 100%;
				background: $uni-title-color;
			}
		}
		.goods_name{
			width: 100%;
			line-height: 40rpx;
			font-synthesis: 24rpx;
			margin-top: 10rpx;
			@include simpleOmit();
		}
		.goods_price_box{
			line-height: 40rpx;
			width: 100%;
			margin-top: 12rpx;
			display: flex;
			align-items: center;
			.sale_price{
				font-size: 28rpx;
				color: red;
				font-weight: bold;
			}
			.market_price{
				font-size: 22rpx;
				color: #C0C0C0;
				text-decoration: line-through;
				margin-left: 14rpx;
			}
				
		}
		.goods_label{
			width: 100%;
			display: flex;
			align-items: center;
			margin-top: 14rpx;
			.common_label{
				border: 1px solid $uni-title-color;
				color: $uni-title-color;
				border-radius: 16rpx;
				height: 36rpx;
				margin-right: 20rpx;
				padding:0 10rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				&>text{
					font-size: 8px !important;
					line-height: 30rpx;
				}
			}
		}
			
	}
</style>
