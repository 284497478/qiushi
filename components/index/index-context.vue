<template>
	<view class="index-context animated bounceIn">
		<view class="index-context-info u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<view><image :src="item.userPic" mode="widthFix"></image></view>
				<text>{{item.nickName}}</text>
			</view>
			<view class="u-f-ac" v-show="!isguanzhu">
				<view class="icon iconfont icon-zengjia" @tap="onFocus">关注</view>
				<!-- <view class="icon iconfont icon-guanbi"></view> -->
			</view>
		</view>
		<view class="index-context-title" @tap="openDetail">
			<text>{{ item.title }}</text>
		</view>
		<view class="index-context-image u-f-ajc" @tap="openDetail">
			<image :src="item.titlePic" mode="widthFix"></image>
			<template v-if="item.type == 'video'">
				<view class="icon iconfont icon-bofang index-context-image-play"></view>
				<view class="index-context-image-playinfo">{{ item.playnum }}次播放 {{ item.long }}</view>
			</template>
		</view>
		<view class="index-context-like u-f-jsb u-f-ac">
			<view class="u-f-ac">
				<view class="icon iconfont icon-icon_xiaolian-mian" :class="{'dingClass' : infoNum.infoType == 1 }" @tap="opreation(1)"></view>
				<text :class="{ 'dingClass' : infoNum.infoType == 1 }">{{ infoNum.dingNum }}</text>
				<view class="icon iconfont icon-kulian" :class="{'caiClass' : infoNum.infoType == 2 }" @tap="opreation(2)"></view>
				<text :class="{'caiClass' : infoNum.infoType == 2 }">{{ infoNum.caiNum }}</text>
			</view>
			<view class="u-f-ac">
				<view class="icon iconfont icon-pinglun"></view>
				<text>{{ item.commentNum }}</text>
				<view class="icon iconfont icon-zhuanfa"></view>
				<text>{{ item.shareNum }}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
				isguanzhu:this.item.isFocusOn,
				infoNum:this.item.infoNum
			};
		},
		methods:{
			onFocus(){
				this.isguanzhu =true;
				uni.showToast({
					title: '关注成功！'
				});
				
			},
			opreation(type){
				// infoNum: {
				// 	infoType: 1, //0,无操作，1：顶，2：踩
				// 	dingNum: 10,
				// 	caiNum: 22
				// },
				switch (type){
					case 1:
						if(this.infoNum.infoType == 1 ) {return};
						this.infoNum.dingNum ++;
						if(this.infoNum.infoType == 2){
							this.infoNum.caiNum--;
						}
						this.infoNum.infoType =1;
						
						break;
					case 2:
						if(this.infoNum.infoType == 2 ) {return};
						this.infoNum.caiNum ++;
						if(this.infoNum.infoType == 1){
							this.infoNum.dingNum--;
						}
						this.infoNum.infoType =2;
						break;
					default:
						break;
				}
			},
			openDetail(){
				uni.navigateTo({
					url: '../../pages/detail/detail?detailData='+JSON.stringify(this.item)
				});
			}
		}
	}
</script>

<style scoped>
	.index-context {
		padding: 45upx;
		border-bottom: 1upx solid #999999;
	}
	
	.index-context-info > view:last-child > view:first-child {
		background-color: #f4f4f4;
		font-size: 32upx;
		padding: 0 10upx;
		border-radius: 10upx;
	}
	
	.index-context-info > view > text {
		margin-left: 20upx;
		font-size: 32upx;
		color: #9a9a9a;
	}
	.index-context-info > view > view:last-child {
		margin-left: 15upx;
		color: #9a9a9a;
	}
	
	.index-context-info > view image {
		width: 80upx;
		height: 80upx;
		border-radius: 100%;
	}
	.index-context-title {
		font-size: 40upx;
		font-weight: bold;
		margin-bottom: 15upx;
	}
	.index-context-image {
		position: relative;
	}
	.index-context-image image {
		width: 100%;
		border-radius: 10upx;
	}
	
	.index-context-like > view > view,
	.index-context-like text {
		color: #9a9a9a;
		margin-left: 10upx;
	}
	.index-context-image-play {
		font-size: 140upx;
		position: absolute;
		color: #ffffff;
	}
	.index-context-image-playinfo {
		position: absolute;
		bottom: 20upx;
		right: 20upx;
		background-color: rgba(51, 51, 51, 0.52);
		border-radius: 40upx;
		font-size: 25upx;
		padding: 0 20upx;
		color: #ffffff;
	}
	
	.dingClass,
	.caiClass {
		color: #ffb400 !important;
	}

</style>
