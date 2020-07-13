<template>
	<view class="topic-new-list animated fade-in fast"  @click="openDetail">
			<image :src="topicNew.titlepic" lazy-load mode="widthFix"></image>
			<view>
				<view class="">#{{topicNew.title}}#</view>
				<view class="">{{topicNew.titledesc}}</view>
				<view class="">动态 {{topicNew.totalnum}} 今日 {{topicNew.todaynum}}</view>
			</view>
	</view>
</template>

<script>
	export default {
		props:{
			topicNew:Object
		},
		methods:{
			openDetail(){
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail'
				});
			}
		}
	}
</script>

<style scoped>
	
/* 最近更新 */

.topic-new-list image{
	
	height: 180upx;
	width: 180upx;
	border-radius: 20upx;
	margin-right: 20upx;
}

.topic-new-list {
	display: flex;
	align-items: center;
	border-bottom: 1upx solid #EFEFEF;
	padding: 20upx 0;
}
.topic-new-list>view>view {
	color: #9D9D9D;
}
.topic-new-list>view>view:first-child{
	
	font-size: 32upx;
	color: #000000;
	
}

</style>
