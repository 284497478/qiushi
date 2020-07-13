<template>
	<view style="margin-left: 100upx;">
		<view class="view-class-demo animated " hover-stay-time="3000"
		hover-class="view-class-demo-hover bounceIn">我的第一个view</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.view-class-demo {
		
		width: 200upx;
		height: 200upx;
		background-color: #007AFF;
	}
	.view-class-demo-hover {
		background-color: #4CD964;
	}

</style>
