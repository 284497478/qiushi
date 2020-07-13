<template>
	<view class="common-list">
		<!-- 左边头像 -->
		<view class="common-list-left"><image :src="item.userpic" mode="aspectFill"></image></view>
		<!-- 右边内容 -->
		<view class="common-list-right">
			<!-- 第一行信息：昵称、性别、年龄 关注 取消关注 -->
			<view class="common-list-right-basinfo u-f-ajc">
				<view class="u-f-ac">
					{{ item.username }}
					<tag-sex-age :age="item.age" :sex="item.sex"></tag-sex-age>
				</view>
				<view class="icon iconfont icon-zengjia" v-show="!isguanzhu" @tap="isFocusOn()">关注</view>
			</view>
			<view class="common-list-right-day">26天前</view>
			<!-- 第二行标题信息 -->
			<view class="common-list-right-title">{{ item.title }}</view>
			<!-- 第三行影片信息 -->
			<!-- 视频 -->
			<uni-grid :column="3" :showBorder="false" :highlight="true" @change="change" style="margin-bottom: 30upx;">
				<uni-grid-item v-for="(pic,index) in item.morepic" :index="index" :key="index">
					<view class="grid-item-box">
						<image :src="pic" class="image" mode="aspectFill" style="border-radius: 20upx;"/>
						<!-- <text class="text">{{ item.text }}</text> -->
					</view>
					</uni-grid-item>
			</uni-grid>
			<view class="common-list-right-video">
				<view class="u-f-ajc">
					
					<!-- 多个图片展示 -->
					<!-- <block v-for="(pic,index) in item.morepic" :key="index" v-if="!item.video">
						<image :src="pic" mode="widthFix" @tap="showImg(index)"></image>
					</block> -->
					<image v-if="item.video" :src="item.titlepic" mode="widthFix"></image>
					<template v-if="item.video">
						<view class="icon iconfont icon-bofang index-context-image-play"></view>
						<view class="">{{ item.video.looknum }}次播放 {{ item.video.long }}</view>
					</template>
				</view>
			</view>
			<view class="common-list-right-share u-f-ajc" v-if="item.share">
				<view><image :src="item.share.titlepic" mode="aspectFill"></image></view>
				<view>{{ item.share.title }}</view>
			</view>

			<!-- 第四行位置及转发评论信息 -->
			<view class="common-list-right-moreinfo u-f-ajc">
				<view class="common-list-right-moreinfo-left">{{ item.path }}</view>
				<view class="common-list-right-moreinfo-right u-f-ajc">
					<view class="icon iconfont icon-zhuanfa"></view>
					{{ item.sharenum }}
					<view class="icon iconfont icon-pinglun1"></view>
					{{ item.commentnum }}
					<view class="icon iconfont icon-ccdbaa"></view>
					{{ item.goodnum }}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
import tagSexAge from '../common/tag-sex-age.vue';
import uniGrid from '../uni-grid/uni-grid.vue'
import uniGridItem from '../uni-grid-item/uni-grid-item.vue'

export default {
	components: {
		tagSexAge,
		uniGrid,
		uniGridItem,
	},
	props:{
		item:Object
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
		},
		showImg(index){

			uni.previewImage({
				urls: this.item.morepic,
				loop:true,
				current:index,
				longPressActions: {
					itemList: ['发送给朋友', '保存图片', '收藏'],
					success: (data)=> {
						console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
					},
					fail:(err)=> {
						console.log(err.errMsg);
					}
				}
			});

		},
		change(e){
			uni.previewImage({
				urls: this.item.morepic,
				loop:true,
				current:e.detail.index,
				longPressActions: {
					itemList: ['发送给朋友', '保存图片', '收藏'],
					success: (data)=> {
						console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data.index + 1) + '张图片');
					},
					fail:(err)=> {
						console.log(err.errMsg);
					}
				}
			});
		}

	},
	mounted() {
		// console.log(JSON.stringify(this.item));
	}
}
</script>

<style scoped>
@import url('../../common/list.css');

.common-list {
	border-bottom: 1upx solid #f0f0f0;
}

.common-list-right {
	border: 0;
}

.common-list-right-day {
	color: #d1d1d1;
	font-size: 25upx;
}
.grid-item-box {
		flex: 1;
		/* position: relative;
 */
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 15px 0;
	}
	.image {
		width: 180upx;
		height: 180upx;
	}
</style>

