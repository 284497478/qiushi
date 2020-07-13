<template>
	<view>
		<!-- 分类导航 -->
		<indexTabBar :tabBars="tabBars" :currenTabBarIndex="currenTabBarindex" @changeTabBarIndex="ontabtapEvent"></indexTabBar>
		<!-- 详细信息 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height: swiperHeight +'px'}" :current="currenTabBarindex" @change="swiperChange" skip-hidden-item-layout="true">
				<swiper-item v-for="(topic ,topicIndex) in topicList" :key="topicIndex" >
					<scroll-view scroll-y class="list" @scrolltolower="loadMoreInfo(topicIndex)" >
						<template v-if="topic.topicContext.length >0">
						<!-- 内容展示组件 -->
						<view class="topic-view">
							<block v-for="(item, index) in topic.topicContext" :key="index">
								<topic-list :topicNew="item"></topic-list>
							</block>
						</view>
						<!-- 加载提示组件 -->
						<loadMore :loadMoreText="topic.loadMorText"></loadMore>
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
	
	import indexTabBar from '../../components/index/index-tabbar.vue';
	import loadMore from '../../components/common/load-more.vue';
	import nothing from '../../components/common/no-thing.vue';
	import topicList from '../../components/news/topic-list.vue';
	
	export default {
		components:{
			indexTabBar,
			loadMore,
			nothing,
			topicList
			
		},
		data() {
			return {
				swiperHeight:500,
				currenTabBarindex:0,
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
				topicList:[
					{
						loadMorText:"上拉加载更多...",
						topicContext: [
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
					},{
						loadMorText:"上拉加载更多...",
						topicContext: [
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
					},{
						loadMorText:"上拉加载更多...",
						topicContext: [
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
					},{
						loadMorText:"上拉加载更多...",
						topicContext: [
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
					},{
						loadMorText:"上拉加载更多...",
						topicContext: []
					},{
						loadMorText:"上拉加载更多...",
						topicContext: []
					},{
						loadMorText:"上拉加载更多...",
						topicContext: []
					}
				]
			}
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
			ontabtapEvent(index){
				this.currenTabBarindex = index;
			},
			swiperChange(e){
				this.currenTabBarindex = e.detail.current;
				this.times =1;
			
			},
			loadMoreInfo(topicIndex){
				if(this.topicList[topicIndex].loadMorText != "上拉加载更多..."){
					return ;
				}
				this.topicList[topicIndex].loadMorText = "加载中.."
				let loadResult = setTimeout(()=> {
					
					let tmpObj = {
								titlepic:"../../static/demo/topicpic/14.jpeg",
								title:"淘宝记录簿",
								titledesc:"120斤到85斤 我的人生反转",
								totalnum:40,
								tadaynum:20
							};
							
					this.topicList[topicIndex].topicContext.push(tmpObj);
					
					this.times--;
					if(this.times == 0 ){
						this.topicList[topicIndex].loadMorText = "没有更多数据了";
					}else{
						this.topicList[topicIndex].loadMorText = "上拉加载更多...";
					}
					
				}, 5000);
				
			}
		}
	}
</script>

<style scoped>
.topic-view{
	padding: 0 20upx;
}

</style>
