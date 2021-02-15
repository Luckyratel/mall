<template>
	<view class="feature_box" :style="customStyle">
		<view class="feature_title" v-if="!titleHide">
			<view class="feature_title_left" v-if="titleText">
				<text>{{titleText}}</text>
			</view>
			<view class="feature_title_right" v-if="titleLabel">
				<text>{{titleLabel}}</text>
				<i class="iconfont iconright"></i>
			</view>
		</view>
		<view class="feature_content">
			<view class="feature_content_mode1" v-if="mode == 'normal'">
				<block v-for="(item, index) in 10" :key="index">
					<view class="common_feature" :style="{'width': defaultWidth}">
						<view class="feature_img" :style="{'width': defaultWidth}">
							<image style="height: 40rpx;width: 40rpx; background: #007AFF;"></image>
						</view>
						<text>功能1</text>
					</view>
				</block>
			</view>

			<swiper class="swiper_box" :style="{'height': swiperHeight}" indicator-color="#C0C0C0" indicator-dots="true" indicator-active-color="#dd524d">
				<swiper-item>
					<view class="feature_content_mode1" style="margin-top: 0rpx;" v-if="mode == 'swiper'">
						<block v-for="(item, index) in 5" :key="index">
							<view class="common_feature" :style="{'width': defaultWidth}">
								<view class="feature_img" :style="{'width': defaultWidth}">
									<image style="height: 40rpx;width: 40rpx; background: #007AFF;"></image>
								</view>
								<text>功能1</text>
							</view>
						</block>
					</view>
				</swiper-item>
			</swiper>

		</view>
	</view>
</template>

<script>
	export default {
		props: {
			customStyle: Object,
			line: { //每行个数
				type: Number | String,
				default: 5
			},
			mode: { // 模式 noraml 和 swiper
				type: String,
				default: 'normal'
			},
			titleHide: { // 是否显示 主题
				type: Boolean,
				default: false
			},
			textHide: { // 是否显示功能文字
				type: Boolean,
				default: false
			},
			titleText: String, // 主题文字
			titleLabel: String, // 主题右边的标签文字
			swiperHeight: String // 轮播高度
		},
		computed: {
			"defaultWidth": function() {
				let weight = 100 / this.line;
				console.log(weight);
				return (weight + '%');
			},
		}
	}
</script>

<style lang="scss">
	.feature_box {
		width: 100%;
		padding: 20rpx 0rpx;
		background: #FFFFFF;

		.feature_title {
			width: 100%;
			display: flex;
			align-items: center;
			justify-content: space-between;

			.feature_title_left {
				margin-left: 20rpx;
				font-size: 30rpx;
				color: #000000;
				font-weight: bold;

			}

			.feature_title_right {
				margin-right: 20rpx;
				font-size: 26rpx;
				color: #C0C0C0;
			}
		}
		.swiper_box {
			width: 100%;
		}
		.feature_content {
			width: 100%;

			.feature_content_mode1 {
				display: flex;
				flex-wrap: wrap;
				margin-top: 20rpx;

				.common_feature {
					display: flex;
					align-items: center;
					flex-direction: column;
					justify-content: center;
					padding-top: 20rpx;
					padding-bottom: 20rpx;

					.feature_img {
						display: flex;
						align-items: center;
						flex-direction: column;
						justify-content: center;
					}

					&>text {
						font-size: 24rpx;
						color: #C0C0C0;
						margin-top: 14rpx;
					}
				}

			}
		}
	}
</style>
