<template>
	<view>
		<view class="paper-list-popup-mask" v-if="show" @click="hidePopup"></view>
		<view class="paper-list-popup" v-if="show">
			<view class="u-f-ac" hover-class="paper-list-popup-h" @click="addfriend">
				<view class="icon iconfont icon-sousuo"></view>加糗友
			</view>
			<view class="u-f-ac" hover-class="paper-list-popup-h" @click="clear">
				<view class="icon iconfont icon-qingchu"></view>清空未读
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			show:Boolean
		},
		methods:{
		
			hidePopup(){
				this.$emit("hide");
			},
			addfriend(){
				this.$emit('addfriend');
			},
			clear(){
				this.$emit('clear');
			}
			
		}
	}
</script>

<style scoped>
	.paper-list-popup{
		width: 55%;
		position: fixed;
		right: 0;
		background-color: #FFFFFF;
		z-index: 2000;
		top: 5upx;
		box-shadow: 1upx 1upx 20upx 2upx #CCCCCC;
	}
	.paper-list-popup-mask{
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 1999;
	}
	.paper-list-popup>view{
		padding: 20upx 20upx;
		font-size: 35upx;
	}
	.paper-list-popup>view>view{
		
		margin-right: 20upx;
		font-weight: bold;
		
	}
	
	.paper-list-popup-h {
		background-color: #EEEEEE;
	}
</style>
