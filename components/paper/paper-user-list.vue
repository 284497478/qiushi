<template>
	<view class="user-list u-f-ajc">
		<image :src="user.userpic" mode="aspectFill" lazy-load></image>
		<view class="" @click="openChat">
			<view>{{user.username}}</view>
			<view style="display: flex;justify-content: left;">
				<tag-sex-age :age="user.age" :sex="user.sex"></tag-sex-age>
			</view>
		</view>
		<view class="icon iconfont " :class="[user.isguanzhu?'icon-xuanze-yixuan':'icon-zengjia1']"></view>
	</view>
</template>

<script>
	import tagSexAge from '../../components/common/tag-sex-age.vue';
	
	export default {
		components:{
			tagSexAge
		},
		props:{
			user:Object
		},
		methods:{
			openChat(){
				uni.navigateTo({
					url: '../../pages/user-chat/user-chat'
				});
			}
		},
		mounted() {
			// console.log(this.user);
		}
	}
</script>

<style scoped>
	.user-list {
		padding: 20upx 0;
		border-bottom: 1upx solid #ECECEC;
	}
	.user-list>image {
		height: 100upx;
		width: 100upx;
		border-radius: 100%;
		flex-shrink: 0;
		margin-right: 20upx;
	}
	.user-list>view:first-of-type{
		flex: 1;
		overflow: hidden;
		padding: 0 20upx;
		
	}
	.user-list>view:last-of-type {
		width: 80upx;
		color: #CCCCCC;
		flex-shrink: 0;
	}
	.user-list>view>view:first-child {
		font-size: 32upx;
		overflow: hidden;
	}
	.user-list>view>view{
		margin: 10upx 0;
	}
	
	.icon-zengjia1{
		color: #FF6333 !important;
	}
</style>
