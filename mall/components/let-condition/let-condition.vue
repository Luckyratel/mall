<template>
	<view class="let_conditon_box">
		<block v-for="(info, index) in list" :key="index">
			<view class="common_condition" :class="{'orderBy': info.hasOrderBy, 'select': conditionIndex == index}" @tap="selectConditon(index)">
				<text>{{info.label}}</text>
				<view class="orderBy_box" v-if="info.hasOrderBy">
					<image class="up" src="/static/imgs/common/right_red.png" v-if="orderByIndex == 0"></image>
					<image class="up" src="/static/imgs/common/right.png" v-else></image>
					<image class="down" src="/static/imgs/common/right_red.png" v-if="orderByIndex == 1"></image>
					<image class="down" src="/static/imgs/common/right.png" v-else></image>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	const orderByList = ['asc', 'desc']
	export default{
		props:{
			list: Array
		},
		data() {
			return {
				conditionIndex: 0,
				orderByIndex: -1
			}
		},
		methods:{
			selectConditon: function(index){
				let condition = this.list[index];
				if(condition.hasOrderBy){	
					if(this.conditionIndex == index){
						this.conditionIndex = index
						if(this.orderByIndex < 0){
							this.orderByIndex = 0;
						}else{
							this.orderByIndex = this.orderByIndex ? 0 : 1;
						}
					}else{
						this.conditionIndex = index
						this.orderByIndex = 0
					}
				}else{
					this.conditionIndex = index
					this.orderByIndex = -1;
				}
				this.changeHandle();
			},
			changeHandle: function(){
				let orderBy = "";
				if(this.orderByIndex < 0){
					orderBy = ""
				}else{
					orderBy = orderByList[this.orderByIndex];
				}
				this.$emit('change', {
					index: this.conditionIndex,
					orderBy,
				})
			}
		}
	}
</script>

<style lang="scss">
	.let_conditon_box{
		height: 100%;
		min-height: 80rpx;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-around;
		.common_condition{
			font-size: 26rpx;
			color: #333333;
			&.select{
				color: $uni-title-color;
			}
			&.orderBy{
				display: flex;
				align-items: center;
			}
			.orderBy_box{
				display: flex;
				align-items: center;
				justify-content: center;
				flex-direction: column;
				margin-left: 6rpx;
				.up{
					transform: rotate(-90deg);
					height: 30rpx;
					width: 30rpx;
					position: relative;
					bottom: -8rpx;
				}
				.down{
					height: 30rpx;
					width: 30rpx;
					transform: rotate(90deg);
					position: relative;
					top: -4rpx;
				}
			}
		}
	}
</style>
