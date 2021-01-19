<template>
	<view class="com_search_box">
		<view class="com_search_panel">
			<view class="search_icon">
				<i class="iconfont iconsearch"></i>
			</view>
			<input :placeholder="placeholder" :value="inputValue" @input="handleInput" />
		</view>
	</view>
</template>
<!-- 
	第二種父子組件 v-model 通信方式
	<input :placeholder="placeholder" :v-model="value" />
	等同於
	<input :placeholder="placeholder" :value ="value" @input="value = $event.detail.value"/>
 -->
<script>
	export default{
		model:{
			prop:"inputValue", // prop说:我要将value1作为该组件被使用(被父组件调用)时,v-model能取到的值
			event: "change" // event说:我emit(触发)change的时候，参数的值就是父组件v-model收到的值。
		},
		props:{
			placeholder:{
				type: String,
				default: '請輸入關鍵字'
			},
			inputValue: String
		},
		methods:{
			handleInput:function(e){
				this.$emit('change', e.detail.value);
			}
		}
	}
</script>

<style lang="scss">
	.com_search_box{
		height: 100rpx;
		width: 100%;
		background: #FFFFFF;
		.com_search_panel {
			width: calc(100% - 60rpx);
			margin-left: 30rpx;
			height: 60rpx;
			background: #CCCCCC;
			border-radius: 30rpx;
			display: flex;
			align-items: center;
			.search_icon{
				margin-left: 30rpx;
			}
			&>input{
				flex: 1;
				margin: 0 10rpx;
				font-size: 26rpx;
				height: 60rpx;
			}
		}
	}
</style>
