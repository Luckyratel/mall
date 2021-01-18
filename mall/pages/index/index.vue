<template>
	<view class="content">
	
		<!-- <specification></specification> -->
		<let-search v-model="title"></let-search>
		<view>{{title}}</view>
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
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	
</style>
