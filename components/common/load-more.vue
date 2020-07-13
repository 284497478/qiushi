<template>
	<view class="load-text">{{loadMoreText}}</view>
</template>

<script>
	export default {
		props:{
			loadMoreText:String
		}
		// ,
		// mounted() {
		// 	console.log(this.loadMoreText);
		// }
	}
</script>

<style scoped>
	
.load-text {
	
	font-size: 32upx;
	color: #D8D8D8;
	text-align: center;
	margin-top: 20upx;
}


</style>
