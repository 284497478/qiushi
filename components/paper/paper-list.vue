<template>
	<view class="paper-list-detail u-f-ajc animated fadeInLeft fast" @click="openDetail()">
		<image :src="paper.userpic" mode="aspectFill"></image>
		<view class="paper-list-detail-r">
			<view class="paper-list-detail-r-f u-f-ac u-f-jsb">
				{{paper.username}}
				<view>{{paper.time}}</view>
			</view>
			<view class="paper-list-detail-r-t u-f-ac u-f-jsb">
				<view>{{paper.data}}</view>
				<template v-if="paper.noreadnum > 0"></template>
				<view>
					<uni-badge class="uni-badge-left-margin" :size="small" :text="paper.noreadnum" type="error" />
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	
	import uniBadge from '../../components/uni-badge/uni-badge.vue';
	
	export default {
		components:{
			uniBadge
		},
		props:{
			paper:Object,
			index:Number
		},methods:{
			
			openDetail(){
				uni.navigateTo({
					url: '../../pages/user-chat/user-chat'
				});
			}
		}
	}
</script>

<style scoped>
	
	.paper-list-detail{
		border-bottom: 1upx solid #ECECEC;
		padding-bottom: 25upx;
	}
	.paper-list-detail image{
		width: 80upx;
		height: 80upx;
		border-radius: 100%;
		flex-shrink: 0;
		margin-right: 20upx;
	}
	
	.paper-list-detail-r{
		flex: 1;
	}
	
	.paper-list-detail-r-f {
		font-size: 30upx;
	}
	.paper-list-detail-r-f>view {
		font-size: 28upx;
		color: #C2C2C2;
	}
	.paper-list-detail-r-t>view:first-child{
		font-size: 28upx;
		display: -webkit-box;
		-webkit-box-orient:vertical; 
		-webkit-line-clamp:1;
		overflow: hidden;
		color: #979797;
		
	}
</style>
