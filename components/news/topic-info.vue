<template>
	<view>
		<view class="topic-bg">
			<image :src="topicInfo.titlepic" mode="aspectFill"></image>
		</view>
		<view class="topic-info">
			<view class="topic-info-t u-f-ac">
				<view>
					<image :src="topicInfo.titlepic" mode="aspectFill"></image>
				</view>
				<view>#{{topicInfo.title}}#</view>
			</view>
			<view class="topic-info-c u-f-ac">
				<view class="">动态 {{topicInfo.totalnum}}</view>
				<view class="">今日 {{topicInfo.todaynum}}</view>
			</view>
			<view class="topic-info-b">{{topicInfo.titledesc}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			topicInfo:Object
		}
	}
</script>

<style scoped>
	.topic-bg{
		height: 300upx;
		width: 100%;
		/* position: relative; */
		overflow: hidden;
	}
	.topic-bg image {
		height: 300upx;
		width: 100%;
		/* position: absolute; */
		filter: blur(10upx);
	}
	.topic-info-t {
		position: relative;
	}
	
	.topic-info-t image {
		height: 150upx;
		width: 150upx;
		position: absolute;
		top: -75upx;
		border-radius: 20upx;
		margin-left: 30upx;
	}
	.topic-info-t>view:last-child {
		margin-left: 200upx;
		font-size: 35upx;
		flex: 1;
	}
	
	.topic-info-c {
		margin-top: 30upx;
		padding:0 30upx;
		color: #CFCFCF;
		
		
	}
	.topic-info-c>view:last-child {
		margin-left: 20upx;
		
	}
	.topic-info-b {
		margin-top: 20upx;
		padding: 0 30upx;
		color: #9D9D9D;
	}
	
</style>
