<template>
	<view class="user-chat-bottom u-f-ac">
		<input type="text" placeholder="请文明发言" v-model="text"/>
		<view class="icon iconfont icon-fabu" @click="sendMsg"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				text: ""
			}
		},
		methods:{
			sendMsg(text){
				this.$emit("sendMsg",this.text);
				this.text="";
			}
		}
	}
</script>

<style>
	.user-chat-bottom {
		border-top: 1upx solid #EFEFEF;
		padding: 30upx;
		position: fixed;
		right: 0;
		left: 0;
		bottom: 0;
		height: 80upx;
		background-color: #FFFFFF;
	}
	.user-chat-bottom input {
		border-radius: 10upx;
		background-color: #F7F7F7;
		color: #ABABAB;
		margin-right: 20upx;
		height: 70upx;
		flex: 1;
		padding-left: 20upx;
	}
	.user-chat-bottom view {
		font-size: 40upx;
		width: 40upx;
	}
</style>
