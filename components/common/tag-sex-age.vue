<template>
	<view class="common-list-right-basinfo-age u-f-ajc">
		<view class="icon iconfont" :class="[sex == 0 ?'icon-nan':'icon-nv']">{{age}}</view>
	</view>
</template>

<script>
	export default {
		props:{
			sex:Number,
			age:Number
		},
		mounted() {
			// console.log("thisis sex"+this.sex +"："+this.age);
		}
	}
</script>

<style scoped>
	.common-list-right-basinfo-age  {
		color: #FFFFFF;
		padding: 0 5upx;
		margin-left: 8upx;
		overflow: hidden;
	}
	.common-list-right-basinfo-age .icon-nan{
		background-color: #44B3FF;
		line-height: 30upx;
		font-size: 25upx;
		border-radius: 15upx;
		padding: 0 10upx;
	}
	.common-list-right-basinfo-age .icon-nv{
		background-color: #FF698D;
		line-height: 30upx;
		border-radius: 15upx;
		font-size: 25upx;
		padding: 0 10upx;
	}
</style>
