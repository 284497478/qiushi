<template>
	<view class="user-chat-item">
		
		<!-- 聊天信息 -->
		<view v-if="item.gstime" class="user-chat-time u-f-ajc">{{item.gstime}}</view>
		<view class="user-chat-list u-f" :class="{'user-chat-me':item.isme}">
			<image v-if="!item.isme" :src="item.userpic" mode="aspectFill" lazy-load @click="showImg(item.userpic)"></image>
			<view class="user-chat-list-body">
				<!-- 文字 -->
				<text v-if="item.type == 'text'">{{item.data}}</text>
				<!-- 图片 -->
				<image v-if="item.type == 'img'"  :src="item.data" mode="aspectFill" lazy-load @click="showImg(item.data)"></image>
			</view>
			<image v-if="item.isme"  :src="item.userpic" mode="aspectFill" lazy-load @click="showImg(item.userpic)" ></image>
		</view>
		
		<!-- <view v-if="isdspy" class="uset-chat-popus-img">
			<image :src="img" mode="widthFix" lazy-load=""></image>
		</view> -->
		
		<!-- 打开图片 -->
		<view v-if="isdspy"  class="user-chat-showimg u-f-ajc">
			<uni-popup ref="showimage" :type="type" :mask-click="true">
				<view class="uni-image user-chat-showimg-i">
					<image class="image" :src="img" mode="widthFix" />
					<view class="uni-image-close" @click="closeImg()">
						<uni-icons type="clear" color="#fff" size="30" />
					</view>
				</view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
	import uniPopup from '../uni-popup/uni-popup.vue';
	import uniIcons from '@/components/uni-icons/uni-icons.vue';
	export default {
		components: {
			uniPopup,
			uniIcons
		},
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
				type:'',
				isdspy:false,
				img:""
			}
		},
		methods:{
			
			showImg(src){
				this.img = src;
				this.isdspy =true;
				// this.$refs.showimage.open();
				this.$nextTick(() => {
					this.$refs['showimage'].open()
				})
			},
			closeImg(){
				this.isdspy =false;
				this.$refs['showimage'].close();
			}
			
		}
	}
</script>

<style scoped>
	
	.user-chat-list {
		padding: 20upx 20upx;
	}
	.user-chat-list>image{
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		flex-shrink: 0;
		
	}
	
	.user-chat-list-body {
		position: relative;
		background: #F4F4F4;
		padding: 25upx;
		margin-left: 20upx;
		border-radius: 20upx;
		margin-right: 100upx;
	}
	
	
	.user-chat-list-body::after{
		border: 16upx solid #F4F4F4 ;
		position: absolute;
		left:-30upx;
		right: auto;
		top: 30upx;
		content: '';
		width: 0;
		height: 0;
		border-color: transparent #F4F4F4 transparent transparent;
		
		
	}
	
	.user-chat-me{
		justify-content: flex-end;
	}
	.user-chat-me .user-chat-list-body {
		margin-right: 20upx;
		margin-left: 100upx;
	}
	.user-chat-me .user-chat-list-body::after{
		left:auto;
		right: -30upx;
		border-color: transparent transparent transparent #F4F4F4;
	}
	.user-chat-list-body>image {
		max-width: 250upx;
		max-height: 300upx;
	}
	.user-chat-time {
		color: #acacac;
		padding: 50upx 0;
		font-size: 24upx;
	}
	.uni-popup{
		left: 60upx !important;
	}
	
</style>
