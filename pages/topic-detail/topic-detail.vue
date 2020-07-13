<template>
	<view>
		<!-- 话题介绍 -->
		<topic-info :topicInfo="topicInfo">
		</topic-info>
		<!-- 导航组件 -->
		<indexTabBar :tabBars="tabBars" :currenTabBarIndex="currenTabBarindex" @changeTabBarIndex="ontabtapEvent" :scrollStyle="scrollStyle" :scrollItemStyle="scrollItemStyle" class="bord">
		</indexTabBar>
		<!-- 列表 -->
		<view class="topic-detail-list">
			<!-- <block v-for="(tmp,index) in topicData" :key="index"> -->
				<view v-for="(item,listindex) in topicData[currenTabBarindex].itemList" :key="listindex">
					<common-list :item="item" :index="listindex"></common-list>
				</view>
				<!-- </block> -->
				<load-more :loadMoreText="topicData[currenTabBarindex].loadMorText"></load-more>
		</view>
	</view>
</template>

<script>
	import topicInfo from '../../components/news/topic-info.vue';
	import indexTabBar from '../../components/index/index-tabbar.vue';
	import commonList from '../../components/common/common-list.vue';
	import loadMore from '../../components/common/load-more.vue'
	
	export default {
		components: {
			topicInfo,
			indexTabBar,
			commonList,
			loadMore
		},
		onLoad() {
		
		},
		data() {
			return {
				times:3,
				swiperHeight:500,
				scrollStyle:"border-bottom: 0",
				scrollItemStyle:"width:50%",
				topicInfo:{
					titlepic:"../../static/demo/datapic/lvyou4.jpeg",
					title:"忆往事，敬余生",
					titledesc:"面试官：在电梯里巧遇马云你会做什么？90后女孩的回答当场被录用",
					totalnum:"793",
					todaynum:"641"
				},
				tabBars:[
					{
						name:"默认",
						id:"moren"
					},{
						name:"最新",
						id:"zuixin"
					}
				],
				currenTabBarindex:0,
				topicData:[
					{
						loadMorText:"上拉加载更多...",
						itemList:[
								// 文字
								{
									userpic: '../../static/demo/datapic/lvyou4.jpeg',
									username: '哈哈',
									sex: 0, //0 男 1 女
									age: 25,
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
									sex: 0, //0 男 1 女
									age: 25,
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
									age: 25,
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
								}
						]
					},
					{
						loadMorText:"上拉加载更多...",
						itemList:[
								// 文字
								{
									userpic: '../../static/demo/datapic/lvyou8.jpeg',
									username: '哈哈',
									sex: 1, //0 男 1 女
									age: 30,
									isguanzhu: false,
									title: '最新更新内容',
									titlepic: '',
									video: false,
									share: false,
									path: '北京 北京',
									sharenum: 20,
									commentnum: 30,
									goodnum: 20
								},
								// 图文
								{
									userpic: '../../static/demo/datapic/lvyou9.jpeg',
									username: 'Allen',
									sex: 1, //0 男 1 女
									age: 25,
									isguanzhu: false,
									title: '测试',
									titlepic: '../../static/demo/datapic/lvyou8.jpeg',
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
									age: 25,
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
								}
						]
					
					}
				]
			}
		},
		//当前页面触底时发生事件
		onReachBottom() {
			this.loadMoreInfo();
				
		},
		//下拉页面时触发事件
		onPullDownRefresh(){
			setTimeout(()=> {
				let responseInfo = {
					userpic: '../../static/demo/userpic/6.jpg',
					username: '养胖的jiji',
					sex: 0, //0 男 1 女
					age: 32,
					isguanzhu: false,
					title: '流氓显示',
					titlepic: '../../static/demo/datapic/l12.jpeg',
					video: false,
					share: false,
					path: '海南 海口',
					sharenum: 11,
					commentnum: 32,
					goodnum: 44
				}
				
				this.topicData[this.currenTabBarindex].itemList.push(responseInfo);
				
				uni.stopPullDownRefresh();
			}, 3000);
		},
		methods: {
			ontabtapEvent(index){
				this.currenTabBarindex = index;
			},
			loadMoreInfo(){
				if(this.topicData[this.currenTabBarindex].loadMorText != "上拉加载更多..."){
					return ;
				}
				this.topicData[this.currenTabBarindex].loadMorText = "加载中.."
				let loadResult = setTimeout(()=> {
					
					let tmpObj ={
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '../../static/demo/datapic/l11.jpeg',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							};
							
					this.topicData[this.currenTabBarindex].itemList.push(tmpObj);
					
					this.times--;
					if(this.times == 0 ){
						this.topicData[this.currenTabBarindex].loadMorText = "没有更多数据了";
					}else{
						this.topicData[this.currenTabBarindex].loadMorText = "上拉加载更多...";
					}
					
				}, 3000);
				
			}
		}
	}
</script>

<style>

	
</style>
