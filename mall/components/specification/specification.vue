<template>
	<view class="specification_box">
		<view class="mask"></view>
		<view class="specification_info">
			<view class="spec_cancal_icon">
				<i class="iconfont icondelete"></i>
			</view>
			<view class="spec_show_box">
				<view class="show_left">
					<image src="" class="goods_img"></image>
				</view>
				<view class="show_right">
					
					<view class="spec_box">
						<text>已选: </text>
						<view class="spec_text">
							<text>60</text>
						</view>
					</view>
					<view class="spec_stock">
						<text>库存：40</text>
					</view>
					<view class="spec_price">
						<text>价格:￥69</text>
					</view>
				</view>
			</view>
			<view class="spec_select_box">
				<block v-for="(spec, index) in productSpec" :key="index">
					<view class="spec_selec_box">
						<view class="spec_select_label"><text>{{spec.label}}</text></view>
						<view class="spec_selec_item">
							<block v-for="(specText, specIndex) in spec.specValues" :key="specIndex">
								<view class="spec_item_text"> <text>{{specText}}</text> </view>
							</block>
						</view>
					</view>
				</block>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				productIds:[
					[2,4,6],[2,4,7],[3,5,6]
				],
				productSpec:[
					{
						label: '规格',
						specValues: ['大', '小']
					},
					{
						lable: '颜色',
						specValues:['红','蓝']
					},
					{
						label: '重量',
						specValues: ['300g','500g']
					}
				]
			}
		}
	}
</script>

<style lang="scss" scoped="scoped">
	.specification_box{
		position: fixed;
		z-index: 100;
		width: 100%;
		height: 100%;
		.mask{
			height: 100%;
			width: 100%;
			background: #000000;
			opacity: 0.4;
		}
		.specification_info{
			width: 100%;
			background: #FFFFFF;
			position: absolute;
			bottom: 0rpx;
			left: 0rpx;
			.spec_cancal_icon{
				width: 100%;
				height: 60rpx;
				text-align: right;
				&>i{
					font-size: 30rpx;
				}
				&>image{
					height: 40rpx;
					width: 40rpx;
				}
			}
			.spec_show_box{
				display: flex;
				align-items: center;
				box-sizing: border-box;
				padding: 0 20rpx;
				.show_left{
					height: 160rpx;
					width: 160rpx;
					border-radius: 10rpx;
					&>image{
						height: 100%;
						width: 100%;
						background-color: #007AFF;
					}
				}
				.show_right{
					display: flex;
					flex-direction: column-reverse;
					height: 160rpx;
					margin-left: 30rpx;
					.spec_price{
						font-size: 28rpx;
						color: red;
					}
					.spec_stock{
						font-size: 28rpx;
						color: #666666;
					}
					.spec_box{
						display: flex;
						align-items: center;
						flex-wrap: wrap;
						color: #666666;
						font-size: 28rpx;
						margin-bottom: 20rpx;
						.spec_text{
							margin-left: 10rpx;
							font-size: 28rpx;
						}
					}
				}
			}
		}
	}
</style>
