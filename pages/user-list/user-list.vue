<template>
	<view class="body">
		<!-- 分类导航 -->
		<indexTabBar :tabBars="newsItems" :currenTabBarIndex="currentIndex" @changeTabBarIndex="ontabtapEvent" scrollStyle="border-bottom:0" scrollItemStyle="width:33%"></indexTabBar>
		
		
		
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height: swiperHeight +'px'}" :current="currentIndex" @change="swiperChange" skip-hidden-item-layout="true">
				<swiper-item v-for="(paperUser ,paperIndex) in paperUserData" :key="paperIndex" >
					<scroll-view scroll-y class="list" @scrolltolower="loadMoreInfo(paperIndex)" >
						<template v-if="paperUser.userList.length >0">
						<!-- 内容展示组件 -->
						<block v-for="(item, index) in paperUser.userList" :key="index">
							<paper-user-list :user="item"></paper-user-list>
						</block>
						<!-- 加载提示组件 -->
						<loadMore :loadMoreText="paperUser.loadMorText"></loadMore>
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
	import paperUserList from '../../components/paper/paper-user-list.vue';
	import loadMore from '../../components/common/load-more.vue';
	import nothing from '../../components/common/no-thing.vue';
	
	export default {
		components:{
			indexTabBar,
			paperUserList,
			loadMore,
			nothing
		},
		data() {
			return {
				times:3,
				swiperHeight:500,
				currentIndex: 0,
				newsItems: [
					{
						name: '互关',
						id: 'huguan',
						num:10
					},
					{
						name: '关注',
						id: 'guanzhu',
						num:21
					},
					{
						name: '粉丝',
						id: 'fensi',
						num:13
					}
				],
				paperUserData:[
					{
						loadMorText:"上拉加载更多...",
						userList:[
							{
								userpic:"../../static/demo/datapic/lvyou8.jpeg",
								username:"继而文化",
								age:17,
								sex:1,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou1.jpeg",
								username:"fucker",
								age:32,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou2.jpeg",
								username:"godeCHUANG",
								age:22,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou3.jpeg",
								username:"天空之位",
								age:29,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou4.jpeg",
								username:"世界见过",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou5.jpeg",
								username:"jack",
								age:90,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou6.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou7.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou8.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou9.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							}
							
						]
					},{
						loadMorText:"上拉加载更多...",
						userList:[
							{
								userpic:"../../static/demo/datapic/lvyou8.jpeg",
								username:"继而文化",
								age:17,
								sex:1,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou1.jpeg",
								username:"fucker",
								age:32,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou2.jpeg",
								username:"godeCHUANG",
								age:22,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou3.jpeg",
								username:"天空之位",
								age:29,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou4.jpeg",
								username:"世界见过",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou5.jpeg",
								username:"jack",
								age:90,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou6.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							}
							
						]
					},{
						loadMorText:"上拉加载更多...",
						userList:[
							{
								userpic:"../../static/demo/datapic/lvyou8.jpeg",
								username:"继而文化",
								age:17,
								sex:1,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou1.jpeg",
								username:"fucker",
								age:32,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou2.jpeg",
								username:"godeCHUANG",
								age:22,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou3.jpeg",
								username:"天空之位",
								age:29,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou4.jpeg",
								username:"世界见过",
								age:22,
								sex:0,
								isguanzhu:false
							},{
								userpic:"../../static/demo/datapic/lvyou5.jpeg",
								username:"jack",
								age:90,
								sex:1,
								isguanzhu:true
							},{
								userpic:"../../static/demo/datapic/lvyou6.jpeg",
								username:"爱上江山",
								age:22,
								sex:0,
								isguanzhu:false
							}
							
						]
					}
				],
				
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
		onNavigationBarButtonTap(e) {
			if(e.index==0){
				uni.navigateBack({
					delta: 1
				});
			}
		},
		methods: {
			ontabtapEvent(index){
				this.currentIndex = index;
			},
			swiperChange(e){
				this.currentIndex = e.detail.current;
				this.times=2;
			
			},
			loadMoreInfo(paperIndex){
				if(this.paperUserData[paperIndex].loadMorText != "上拉加载更多..."){
					return ;
				}
				this.paperUserData[paperIndex].loadMorText = "加载中.."
				let loadResult = setTimeout(()=> {
					
					let tmpObj = {
								userpic:"../../static/demo/datapic/lvyou8.jpeg",
								username:"loadmore",
								age:99,
								sex:1,
								isguanzhu:false
							};
							
					this.paperUserData[paperIndex].userList.push(tmpObj);
					
					this.times--;
					if(this.times == 0 ){
						this.paperUserData[paperIndex].loadMorText = "没有更多数据了";
					}else{
						this.paperUserData[paperIndex].loadMorText = "上拉加载更多...";
					}
					
				}, 3000);
				
			}
		}
	}
</script>

<style>
	.body{
		padding: 0 20upx;
	}
	

</style>
