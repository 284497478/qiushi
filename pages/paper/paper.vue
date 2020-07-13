<template>
	<view class="paper-list">
		
		<paper-left-popup :show="show"
		@hide="hidePopup" @clear="clear" @addfriend="addfriend"></paper-left-popup>
		
		<!-- 小纸条信息 -->
		<block v-for="(paper,index) in paperList " :key="index">
			<paper-list :paper="paper" :index="index"></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :loadMoreText="loadMorText"></load-more>
	</view>
</template>

<script>
	import paperList from '../../components/paper/paper-list.vue';
	import loadMore from '../../components/common/load-more.vue';
	import paperLeftPopup from '../../components/paper/paper-left-popup.vue';
	export default {
		components:{
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				show:false,
				times:3,
				loadMorText:"上拉加载更多...",
				paperList:[
					{
						userpic:"../../static/demo/datapic/l1.jpeg",
						username:"JIA一勺",
						time:"13:45",
						data:"赵丽颖《知否》一句话打脸，“读书”是一个很好的事情",
						noreadnum:12
					},{
						userpic:"../../static/demo/datapic/l2.jpeg",
						username:"低头看雨",
						time:"02:45",
						data:"六道快手菜谱，好吃又下饭，加人都很喜欢",
						noreadnum:21
					},{
						userpic:"../../static/demo/datapic/l3.jpeg",
						username:"淫荡的老湿",
						time:"13:45",
						data:"如何用手账改变你的一生",
						noreadnum:0
					},{
						userpic:"../../static/demo/datapic/l4.jpeg",
						username:"苍老师的践行者",
						time:"13:45",
						data:"35岁程序员，年后第一天被辞退",
						noreadnum:12
					},
					{
						userpic:"../../static/demo/datapic/l1.jpeg",
						username:"JIA一勺",
						time:"13:45",
						data:"赵丽颖《知否》一句话打脸，“读书”是一个很好的事情",
						noreadnum:12
					},{
						userpic:"../../static/demo/datapic/l2.jpeg",
						username:"低头看雨",
						time:"02:45",
						data:"六道快手菜谱，好吃又下饭，加人都很喜欢",
						noreadnum:21
					},{
						userpic:"../../static/demo/datapic/l3.jpeg",
						username:"淫荡的老湿",
						time:"13:45",
						data:"如何用手账改变你的一生",
						noreadnum:0
					},{
						userpic:"../../static/demo/datapic/l4.jpeg",
						username:"苍老师的践行者",
						time:"13:45",
						data:"35岁程序员，年后第一天被辞退",
						noreadnum:12
					},
					{
						userpic:"../../static/demo/datapic/l1.jpeg",
						username:"JIA一勺",
						time:"13:45",
						data:"赵丽颖《知否》一句话打脸，“读书”是一个很好的事情",
						noreadnum:12
					},{
						userpic:"../../static/demo/datapic/l2.jpeg",
						username:"低头看雨",
						time:"02:45",
						data:"六道快手菜谱，好吃又下饭，加人都很喜欢",
						noreadnum:21
					},{
						userpic:"../../static/demo/datapic/l3.jpeg",
						username:"淫荡的老湿",
						time:"13:45",
						data:"如何用手账改变你的一生",
						noreadnum:0
					},{
						userpic:"../../static/demo/datapic/l4.jpeg",
						username:"苍老师的践行者",
						time:"13:45",
						data:"35岁程序员，年后第一天被辞退",
						noreadnum:12
					}
				
				]
			}
		},
		onPullDownRefresh() {
			this.getData();
			
		},
		onReachBottom() {
			this.loadmore();
		},
		onNavigationBarButtonTap(e) {
			switch (e.index){
				case 0:
					console.log("点击了好友列表..");
					uni.navigateTo({
						url: '../user-list/user-list'
					});
					this.hidePopup();
					break;
				case 1:
					this.showPopup();
					console.log("点击了加号..");
					break;
				
			}
		},
		methods: {
			showPopup(){
				this.show=true;
			},
			hidePopup(){
				this.show=false;
			},
			clear(){
				console.log("清空未读..");
				this.hidePopup();
			},
			addfriend(){
				console.log("加糗友...");
				this.hidePopup();
			},
			loadmore(){
			
				if(this.loadMorText != "上拉加载更多..."){
					return ;
				}
				this.loadMorText = "加载中.."
				let loadResult = setTimeout(()=> {
					
					let tmpObj ={
									userpic:"../../static/demo/datapic/l5.jpeg",
									username:"苍老师的践行者",
									time:"13:45",
									data:"35岁程序员，年后第一天被辞退",
									noreadnum:1000
							};
							
					this.paperList.push(tmpObj);
					
					this.times--;
					if(this.times == 0 ){
						this.loadMorText = "没有更多数据了";
					}else{
						this.loadMorText = "上拉加载更多...";
					}
					
				}, 3000);
				
				
			},
			getData(){
				setTimeout(()=> {
					//服务器获取数据
					let resData=[
					{
						userpic:"../../static/demo/datapic/l1.jpeg",
						username:"JIA一勺",
						time:"13:45",
						data:"赵丽颖《知否》一句话打脸，“读书”是一个很好的事情",
						noreadnum:0
					},{
						userpic:"../../static/demo/datapic/l2.jpeg",
						username:"低头看雨",
						time:"02:45",
						data:"六道快手菜谱，好吃又下饭，加人都很喜欢",
						noreadnum:0
					},{
						userpic:"../../static/demo/datapic/l3.jpeg",
						username:"淫荡的老湿",
						time:"13:45",
						data:"如何用手账改变你的一生",
						noreadnum:1
					},{
						userpic:"../../static/demo/datapic/l4.jpeg",
						username:"苍老师的践行者",
						time:"13:45",
						data:"35岁程序员，年后第一天被辞退",
						noreadnum:2
					}
				]
					// 接收数据
					// 赋值
					this.paperList = resData;
					// 停止刷新
					uni.stopPullDownRefresh();
					
				}, 2000);
				
			}
		}
	}
</script>

<style>
	.paper-list {
		padding: 0 25upx;
	}
	
</style>
