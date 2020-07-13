<template>
	<view class="topic-hot-category">
		<view class="u-f-ac u-f-jsb">
			<view>热门分类</view>
			<view class="u-f-ajc" @click="openTopicCategory">更多<view class="icon iconfont icon-jinru"></view></view>
		</view>
		<view class="u-f-ajc">
			<block v-for="(category ,index) in hotCategory" :key="index">
				<view class="u-f-ajc">{{category.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			hotCategory:Array
		},
		methods:{
			openTopicCategory(){
				uni.navigateTo({
					url: '../../pages/topic-nav/topic-nav'
				});
			}
		}
	}
</script>

<style scoped>
	/* 热门分类 */
	.topic-hot-category {
		
		padding: 5upx 20upx;
		border-top: 1upx solid #EDEDED;
		border-bottom: 1upx solid #EDEDED;
		
	}
	.topic-hot-category>view{
	
		font-size: 32upx;
		margin: 20upx 0;
	}
	.topic-hot-category>view:first-child>view:last-child{
		color: #D3D3D3;
	}
	
	.topic-hot-category>view:last-child {
		width: 100%;
		justify-content:space-around;
		
	}
	.topic-hot-category>view:last-child view{
		background-color: #F7F7F7;
		padding: 0upx 20upx;
		border-radius: 10upx;
		color: #A2A2A2;
		
	}
</style>
