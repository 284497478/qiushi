<template>
	<view>
		<!-- 自定义导航栏 -->
		<news-nav-bar :newsItems="newsItems" :currentIndex="currentIndex" @change-item="changeItem"></news-nav-bar>
		
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height: swiperHeight +'px'}" :current="currentIndex" @change="swiperChange" skip-hidden-item-layout="true">
				<!-- 关注内容信息展示 -->
				<swiper-item >
					<scroll-view scroll-y class="list" @scrolltolower="loadMoreInfo" >
						<block v-for="(item, index) in focusOn.itemList" :key="index">
							<common-list :item="item" :index="index"></common-list>
						</block>
						<!-- 加载提示组件 -->
						<loadMore :loadMoreText="focusOn.loadMorText"></loadMore>
					</scroll-view>
				</swiper-item>
				<swiper-item >
					<scroll-view scroll-y class="list" >
						<!-- 搜索框 -->
						<view class="topic-search-view">
							<input class="uni-input" placeholder="搜索话题" placeholder-class="icon iconfont icon-sousuo topic-search-input"  />
						</view>
						<!-- 轮播图 -->
						<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swiper-cls">
							<block v-for="(swiper , index) in topic.swiperImgs" :key="index">
								<swiper-item >
									<image :src="swiper.url" mode="aspectFill"></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<hot-category :hotCategory="topic.hotCategory"></hot-category>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view>最近更新</view>
							<block v-for="(topicNew ,index) in topic.topicList" :key="index">
								<topic-list :topicNew="topicNew"></topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
	</view>
</template>

<script>
import newsNavBar from '../../components/news/news-nav-bar.vue';
import commonList from '../../components/common/common-list.vue';
import loadMore from '../../components/common/load-more.vue';
import hotCategory from '../../components/news/topic-host-category.vue';
import topicList from '../../components/news/topic-list.vue';



export default {
	components: {
		commonList,
		newsNavBar,
		loadMore,
		hotCategory,
		topicList
	},
	data() {
		return {
			swiperHeight:500,
			newsItems: [
				{
					newItem: '关注',
					id: 'guanzhu'
				},
				{
					newItem: '话题',
					id: 'huati'
				}
			],
			currentIndex: 0,
			times:3,
			focusOn:{
				loadMorText:"上拉加载更多...",
				itemList: [
					// 文字
					{
						userpic: '../../static/demo/datapic/lvyou4.jpeg',
						username: '哈哈',
						sex: 0, //0 男 1 女
						age: 12,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '',
						video: false,
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 图文
					{
						userpic: '../../static/demo/userpic/12.jpg',
						username: '哈哈',
						sex: 1, //0 男 1 女
						age: 23,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '../../static/demo/datapic/13.jpg',
						video: false,
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 视频
					{
						userpic: '../../static/demo/userpic/12.jpg',
						username: '哈哈',
						sex: 0, //0 男 1 女
						age: 13,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '../../static/demo/datapic/13.jpg',
						video: {
							looknum: '20w',
							long: '2:47'
						},
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 分享
					{
						userpic: '../../static/demo/userpic/12.jpg',
						username: '哈哈',
						sex: 0, //0 男 1 女
						age: 12,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '',
						video: false,
						share: {
							title: '我是分享的标题',
							titlepic: '../../static/demo/datapic/lvyou3.jpeg'
						},
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					}
				]
			},
			topic:{
				swiperImgs:[
					{
						url:"../../static/demo/datapic/lvyou1.jpeg"
					},{
						url:"../../static/demo/datapic/lvyou2.jpeg"
					},{
						url:"../../static/demo/datapic/lvyou3.jpeg"
					}
				],
				hotCategory:[
					{
						name:"最新"
					},{
						name:"游戏"
					},{
						name:"打卡"
					},{
						name:"情感"
					},{
						name:"故事"
					},{
						name:"喜爱"
					}
				],
				topicList:[
					{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						tadaynum:20
					},{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						tadaynum:20
					},{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						tadaynum:20
					},
					{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						tadaynum:20
					},{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						tadaynum:20
					},{
						titlepic:"../../static/demo/topicpic/13.jpeg",
						title:"淘宝记录簿",
						titledesc:"120斤到85斤 我的人生反转",
						totalnum:40,
						todaynum:20
					}
				]
			}
		};
	},
	onLoad() {
		uni.getSystemInfo({
		    success: (res)=> {
				let winHeight = res.windowHeight - uni.upx2px(100);
				this.swiperHeight = winHeight;
		    }
		});
	},
	methods: {
		changeItem(index) {
			this.currentIndex = index;
		},
		swiperChange(e){
			this.currentIndex = e.detail.current;
		
		},
		loadMoreInfo(){
			if(this.focusOn.loadMorText != "上拉加载更多..."){
				return ;
			}
			this.focusOn.loadMorText = "加载中.."
			let loadResult = setTimeout(()=> {
				
				let tmpObj ={
							userpic: '../../static/demo/userpic/12.jpg',
							username: '哈哈',
							sex: 0, //0 男 1 女
							age: 25,
							isguanzhu: false,
							title: '我是标题',
							titlepic: '../../static/demo/datapic/lvyou2.jpeg',
							video: false,
							share: false,
							path: '深圳 龙岗',
							sharenum: 20,
							commentnum: 30,
							goodnum: 20
						};
						
				this.focusOn.itemList.push(tmpObj);
				
				this.times--;
				if(this.times == 0 ){
					this.focusOn.loadMorText = "没有更多数据了";
				}else{
					this.focusOn.loadMorText = "上拉加载更多...";
				}
				
			}, 3000);
			
		}
	}
};
</script>

<style>
	
.topic-search-view{
	padding: 20upx;
	
	
}
.topic-search-view>input{
	background-color: #F4F4F4;
	border-radius: 10upx;
}
.topic-search-input{
	
	display: flex;
	justify-content: center;
	font-size: 28upx;
	
}

.swiper-cls {
	padding: 0 20upx 20upx 20upx;
	
}
.swiper-cls image {
	border-radius: 20upx;
	width: 100%;
	height: 100%;
}

.topic-new{
	padding: 20upx;
}

.topic-new>view:first-child{
	padding-bottom: 20upx;
}
</style>
