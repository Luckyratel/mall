<template>
	<view class="content">
	
		<!-- <specification></specification> -->
		<!-- <let-search v-model="title"></let-search> -->
		<!-- <let-condition :list="conditionList" @change="conditonChange"></let-condition> -->
		<let-goods></let-goods>
	</view>
</template>

<script>
	import specification from '@/components/specification/specification.vue'
	export default {
		components:{
			specification
		},
		data() {
			return {
				title: 'Hello',
				conditionList:[
					{
						label: '綜合',
						value: '',
						hasOrderBy: false,
					},
					{
						label: '销量',
						value: '',
						hasOrderBy: false,
					},
					{
						label: '价格',
						value: '',
						hasOrderBy: true,
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
			conditonChange:function(e){
				console.log(e)
			}
		}
	}
</script>

<style>
	
</style>
