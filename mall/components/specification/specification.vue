<template>
	<view class="specification_box">
		<view class="mask"></view>
		<view class="specification_info">
			<view class="spec_cancal_icon">
				<i class="iconfont iconcha"></i>
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
								<view class="spec_item_text" :class="{'select': specText.select, 'able': specText.able}" @tap="selectValue(index,specIndex)"> <text>{{specText.value}}</text> </view>
							</block>
						</view>
					</view>
				</block>
			</view>
			<view class="spec_quantity_box">
				<view class="spec_quantity_label">数量</view>
				<view class="spec_quantity_panel">
					<quantity></quantity>
				</view>
			</view>
			<view class="spec_feature_box">
				<view class="spec_btns">
					<view class="sure_btn"> <text>确定</text> </view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	var products =[
					{
						label: '规格',
						specValues: [{
							id: 2,
							value: '大'
						}, {
							id: 3,
							value: '小'
						}]
					},
					{
						label: '颜色',
						specValues:[{
							id: 4,
							value: '红'
						},{
							id: 5,
							value: '蓝'
						}]
					},
					{
						label: '重量',
						specValues: [{
							id: 6,
							value: '300g'
						},{
							id: 7,
							value: '500g'
						}]
					}
				]
	import quantity from '@/components/specification/quantityEditor.vue'
	export default{
		components:{
			quantity
		},
		mounted() {
			this.initSpecial();
		},
		data(){
			return{
				selectProductIds:[-1, -1, -1],
				selectProduct:"",
				productIds:[
					[2,4,6],[2,4,7],[2,5,6],[2,5,7],[3,5,6]
				],
				productSpec:[],
				specLocations:[],
			}
		},
		watch:{
			'selectProductIds': function(selectValue){
				this.findAvaliableSpec()
			}
		},
		methods:{
			// 初始化规格选择器
			initSpecial: function(){
				var productSpec = products;
				var specItems = "";
				let findIndex = -1;
				var defaultSpec = [2,4,6];
				for(var i = 0;i < productSpec.length;i++){
					specItems = productSpec[i].specValues;
					for(let j=0; j<specItems.length; j++){
						if(specItems[j].id == defaultSpec[i]){
							specItems[j]['select'] = true;
						}
						else{
							specItems[j]['select'] = false;
						}
						specItems[j]['able'] = true;
					}
				}
				this.$set(this, 'productSpec', productSpec);
				this.$set(this, 'selectProductIds', defaultSpec);
				this.getSpecLocation();
			},
			// 获取规格位置
			getSpecLocation:function(){
				let location = {
					index: -1,
					specIndex: -1,
					id: -1
				}
				let productSpec = this.productSpec;
				let specValues = [];
				let specLocation = [];
				for(let i=0; i<productSpec.length; i++){
					specValues = productSpec[i].specValues;
					for(let j=0; j<specValues.length; j++){
						location = Object.assign({}, location);
						location.index = i;
						location.specIndex = j;
						location.id = specValues[j].id;
						specLocation.push(location);
					}
				}
				this.specLocations = specLocation;
			},
			// 选择规格
			selectValue:function(index, specIndex){
				var selectProductIds = this.selectProductIds;
				let productSpec = this.productSpec;
				var spec = productSpec[index].specValues;
				if(spec[specIndex].select){
					selectProductIds[index] = -1;
					spec[specIndex].select = false;
				}else{
					for(let j=0; j<spec.length; j++){
						spec[j].select = false;
					}
					selectProductIds[index] = spec[specIndex].id;
					spec[specIndex].select = true;
				}
				productSpec[index].specValues = spec;
				this.selectProductIds = selectProductIds;
				this.productSpec = productSpec;
				this.$nextTick(() => {
					this.findAvaliableSpec();
				})
				this.$forceUpdate()
				
			},
			// 筛选有效项
			findAvaliableSpec: function(){
				let productSpec = JSON.parse(JSON.stringify(this.productSpec));
				let productIds = JSON.parse(JSON.stringify(this.productIds));
				let selectIds = JSON.parse(JSON.stringify(this.selectProductIds));
				let specLocations = this.specLocations;
				let avaliabeSelectIds = [];
				let avaliableIds1 = []; // 有效值1
				let avaliableIds2 = []; // 有效值2
				let specItems = [];
				for(let i=0; i<selectIds.length; i++){
					if(selectIds[i] >= 0){
						avaliabeSelectIds.push(selectIds[i]);
					}
				}
				if(avaliabeSelectIds.length <= 0){
					return
				}
				else{
					avaliableIds1 = this.containRelation(productIds, avaliabeSelectIds);
					if(avaliabeSelectIds.length > 1){
						let avaliabeSelectIdsTemp = [];
						let location = {};
						// 有效值的范围参数
						let avaliableRange = [];
						let specValuesTem = [];
						for(let i=0; i<avaliabeSelectIds.length; i++){
							avaliabeSelectIdsTemp = [];
							for(let j=0; j<avaliabeSelectIds.length; j++){
								if(i != j){
									avaliabeSelectIdsTemp.push(avaliabeSelectIds[j])
								}	
							}
							for(let k=0; k<specLocations.length;k++){
								if(specLocations[k].id == avaliabeSelectIds[i]){
									location = specLocations[k];
								}
							}
							
							specValuesTem = this.productSpec[location.index].specValues;
							for(let n=0; n<specValuesTem.length; n++){
								avaliableRange.push(specValuesTem[n].id);
							}
							
							avaliableIds2 = avaliableIds2.concat(this.containRelation(productIds, avaliabeSelectIdsTemp));
						}
						avaliableIds1 = avaliableIds1.concat(this.intersectionHandle(avaliableRange, avaliableIds2));
					}
					else{
						let selectIndex = -1;
						for(let i=0; i<products.length;i++ ){
							specItems = products[i].specValues;
							if(specItems.indexOf(avaliabeSelectIds[0]) >= 0){
								for(let j=0;j<specItems.length;j++){
									avaliableIds1.push(specItems[j].id);
								}
							}
						}
						avaliableIds1 = avaliableIds1.concat(this.containRelation(productIds, avaliabeSelectIds))
					}
				}
				console.log(avaliableIds1);
				this.invalidHandle(avaliableIds1);
			}, 
			// 根据有效值判断无效的
			invalidHandle:function(effectiveArray){
				let specLocations = this.specLocations;
				let productSpec = JSON.parse(JSON.stringify(this.productSpec));
				let effectiveList = [];
				let specValues = [];
				let location = {};
				// 初始化处理, 默认都无效
				for(let i=0; i<productSpec.length; i++){
					specValues = productSpec[i].specValues;
					for(let j=0; j<specValues.length; j++){
						specValues[j].able = false;
					}
				}
				// 去重处理
				for(let i=0; i<effectiveArray.length; i++){
					if(effectiveList.indexOf(effectiveArray[i]) >= 0){
						continue;
					}
					else{
						effectiveList.push(effectiveArray[i]);
					}
				}
				for(let i=0; i<effectiveList.length; i++){
					for(let j=0; j<specLocations.length;j++){
						if(effectiveList[i] == specLocations[j].id){
							location = specLocations[j];
							productSpec[location.index].specValues[location.specIndex].able = true;
						}
					}
				}
				this.productSpec = productSpec;
			},
			// 数组交集关系
			intersectionHandle:function(arrayParam1, arrayParam2){
				let resultArray = [];
				let findIndex = -1;
				for(let i=0; i<arrayParam1.length; i++){
					findIndex = arrayParam2.indexOf(arrayParam1[i]);
					if(findIndex >= 0){
						resultArray.push(arrayParam1[i]);
					}
				}
				return resultArray;
			},
			// 是否是包含关系
			containRelation: function(originData, compareData){
				let count = 0;
				let resultArray = [];
				let findIndex = -1;
				let findData = [];
				for(var i=0; i<originData.length; i++){
					findIndex = originData[i].indexOf(compareData[0])
					count = 0;
					if(findIndex >= 0){
						findData = originData[i];
						for(let j=0; j<compareData.length; j++){
							if(findData.indexOf(compareData[j]) >= 0){
								count ++;
							}
						}
						if(count == compareData.length){
							resultArray = resultArray.concat(findData);
						}
					}
				}
				// console.log(compareData);
				// console.log(resultArray);
				return resultArray;
			},
		}
	}
</script>

<style lang="scss" scoped="scoped">
	.specification_box{
		position: fixed;
		z-index: 100;
		width: 100%;
		height: 100%;
		top: 0rpx;
		left: 0rpx;
		
		.mask{
			height: 100%;
			width: 100%;
			background: #000000;
			opacity: 0.4;
		}
		.specification_info{
			padding-bottom: 30rpx;
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
					margin: 20rpx;
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
			.spec_select_box{
				width: 100%;
				padding: 0 20rpx;
				box-sizing: border-box;
				.spec_selec_box{
					width: 100%;
					margin-top: 40rpx;
					.spec_select_label{
						font-size: 26rpx;
						color: $uni-text-color;
					}
					.spec_selec_item{
						width: 100%;
						display: flex;
						align-items: center;
						flex-wrap: wrap;
						.spec_item_text{
							margin-top: 20rpx;
							margin-right: 20rpx;
							height: 60rpx;
							line-height: 60rpx;
							padding: 0 20rpx;
							color: #E6E6E6;
							font-size: 24rpx;
							border: 1px solid #E6E6E6;
							&.select{
								border: 0rpx !important;
								background-color: $uni-title-color;
								color: #FFFFFF !important;
							}
							&.able{
								border: 1px solid $uni-border-color;
								color: $uni-text-color;
							}
						}
					}
				}
				
			}
			
			.spec_quantity_box{
				width: 100%;
				margin-top: 20rpx;
				.spec_quantity_label{
					font-size: 26rpx;
					width: 100%;
					box-sizing: border-box;
					padding-left: 20rpx;
					margin-top: 20rpx;
				}
				.spec_quantity_panel{
					margin-top: 20rpx;
				}
			}
			.spec_feature_box{
				width: 100%;
				margin-top: 40rpx;
				margin-bottom: 10rpx;
				.sure_btn{
					height: 90rpx;
					line-height: 90rpx;
					background: $uni-title-color;
					width: calc(100% - 40rpx);
					margin-left: 20rpx;
					border-radius: 40rpx;
					color: #FFFFFF;
					text-align: center;
					font-size: 28rpx;
				}
			}
			
		}
	}
</style>
