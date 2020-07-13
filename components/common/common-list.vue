<template>
	<view class="common-list">
		<!-- 左边头像 -->
		<view class="common-list-left">
			<image :src="item.userpic" mode="aspectFill"></image>
		</view>
		<!-- 右边内容 -->
		<view class="common-list-right">
			<!-- 第一行信息：昵称、性别、年龄 关注 取消关注 -->
			<view class="common-list-right-basinfo u-f-ajc">
				<view class="u-f-ac">
					{{item.username}}
				<tag-sex-age :age="item.age" :sex="item.sex"></tag-sex-age>
				</view>
				<view class="icon iconfont icon-zengjia" v-show="!isguanzhu" @tap="isFocusOn()">关注</view>
			</view>
			<!-- 第二行标题信息 -->
			<view class="common-list-right-title">{{item.title}}</view>
			<!-- 第三行影片信息 -->
			<!-- 视频 -->
			
			<view class="common-list-right-video">
				<view class="u-f-ajc">
					
					<image :src="item.titlepic" mode="widthFix" v-if="item.titlepic"></image>
					<template v-if="item.video">
						<view class="icon iconfont icon-bofang index-context-image-play"></view>
						<view class="">{{item.video.looknum}}次播放 {{item.video.long}}</view>
					</template>
				</view>
			</view>
			<view class="common-list-right-share u-f-ajc" v-if="item.share">
				<view>
					<image :src="item.share.titlepic" mode="aspectFill"></image>
				</view>
				<view>
					{{item.share.title}}
				</view>
				
			</view>
			
			
			<!-- 第四行位置及转发评论信息 -->
			<view class="common-list-right-moreinfo u-f-ajc">
				<view class="common-list-right-moreinfo-left">{{item.path}}</view>
				<view class="common-list-right-moreinfo-right u-f-ajc">
					<view class="icon iconfont icon-zhuanfa"></view>{{item.sharenum}}
					<view class="icon iconfont icon-pinglun1"></view>{{item.commentnum}}
					<view class="icon iconfont icon-ccdbaa"></view>{{item.goodnum}}
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	import tagSexAge from './tag-sex-age.vue';
	
	export default {
		components: {
			tagSexAge
		},
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
				isguanzhu:this.item.isguanzhu
			};
		},
		methods:{
			isFocusOn(){
				this.isguanzhu = true;
				uni.showToast({
					title: '关注成功'
				});
			}
			
		},
		mounted() {
			// console.log(JSON.stringify(this.item));
		}
	}
</script>

<style scoped>
	@import url("../../common/list.css");
	
</style>
