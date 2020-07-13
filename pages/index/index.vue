<template>
	<view>
		<indexTabBar :tabBars="tabBars" :currenTabBarIndex="currenTabBarindex" @changeTabBarIndex="ontabtapEvent"></indexTabBar>
		<!-- 详细信息 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height: swiperHeight +'px'}" :current="currenTabBarindex" @change="swiperChange" skip-hidden-item-layout="true">
				<swiper-item v-for="(news ,newsIndex) in newsList" :key="newsIndex" >
					<scroll-view scroll-y class="list" @scrolltolower="loadMoreInfo(newsIndex)" >
						<template v-if="news.indexContext.length >0">
						<!-- 内容展示组件 -->
						<block v-for="(item, index) in news.indexContext" :key="index">
							<indexContext :item="item" :index="index"></indexContext>
						</block>
						<!-- 加载提示组件 -->
						<loadMore :loadMoreText="news.loadMorText"></loadMore>
						</template>
						<!-- 无内容显示 -->
						<template v-else>
							<nothing></nothing>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
import indexContext from '../../components/index/index-context.vue';
import indexTabBar from '../../components/index/index-tabbar.vue';
import loadMore from '../../components/common/load-more.vue';
import nothing from '../../components/common/no-thing.vue';

export default {
	components: {
		indexContext,
		indexTabBar,
		loadMore,
		nothing
	},
	data() {
		return {
			swiperHeight:0,
			currenTabBarindex:0,
			times:3,
			tabBars: [{
			    name: '关注',
			    id: 'guanzhu'
			}, {
			    name: '推荐',
			    id: 'tuijian'
			}, {
			    name: '体育',
			    id: 'tiyu'
			}, {
			    name: '热点',
			    id: 'redian'
			}, {
			    name: '财经',
			    id: 'caijing'
			}, {
			    name: '娱乐',
			    id: 'yule'
			}, {
			    name: '军事',
			    id: 'junshi'
			}],
			newsList:[
				{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: [
						{
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						},
						{
							userPic: '../../static/demo/userpic/7.jpg',
							nickName: '苍老师践行者',
							isFocusOn: true,
							title: '播放有惊喜',
							type: 'video', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/11.jpg',
							playnum: '20w',
							long: '2:47',
							infoNum: {
								infoType: 1, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 22
							},
							commentNum: 12,
							shareNum: 10
						}
					]
				},{
					loadMorText:"上拉加载更多...",
					indexContext: []
				}
			]
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
	// 监听原生导航搜索点击事件
	onNavigationBarSearchInputClicked() {
		uni.navigateTo({
			url:"../search/search"
		})
		
	},
	//监听原生导航按钮点击事件
	onNavigationBarButtonTap(e) {
		if(e.index == 1){
			uni.navigateTo({
				url: '../add-input/add-input'
			});
		}
		
	},
	methods: {
		ontabtapEvent(index){
			this.currenTabBarindex = index;
			
		},
		swiperChange(e){
			this.currenTabBarindex = e.detail.current;
			this.times =1;
		
		},
		loadMoreInfo(newsIndex){
			if(this.newsList[newsIndex].loadMorText != "上拉加载更多..."){
				return ;
			}
			this.newsList[newsIndex].loadMorText = "加载中.."
			let loadResult = setTimeout(()=> {
				
				let tmpObj = {
							userPic: '../../static/demo/userpic/6.jpg',
							nickName: 'Allen',
							isFocusOn: false,
							title: '花瓣的美女就是多',
							type: 'img', //img:图文，video：视频
							titlePic: '../../static/demo/datapic/lvyou4.jpeg',
							infoNum: {
								infoType: 0, //0,无操作，1：顶，2：踩
								dingNum: 10,
								caiNum: 13
							},
							commentNum: 12,
							shareNum: 10
						};
						
				this.newsList[newsIndex].indexContext.push(tmpObj);
				
				this.times--;
				if(this.times == 0 ){
					this.newsList[newsIndex].loadMorText = "没有更多数据了";
				}else{
					this.newsList[newsIndex].loadMorText = "上拉加载更多...";
				}
				
			}, 3000);
			
		}
		
		
	}
};
</script>

<style>
	


</style>
