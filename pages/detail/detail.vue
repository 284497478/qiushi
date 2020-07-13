<template>
	<view id="scrollview">
		<detail-info :item="picitems" @tap="showImg"></detail-info>
		
		<view class="u-comment-title">最新评论 {{comment.count}}</view>
		
		<view class="uni-comment u-comment">
			<block v-for="(item , index ) in comment.list" :key="index">
				<comment-list :item="item" :index="index"></comment-list>
			</block>
		</view>
		<view style="height: 160upx;"></view>
		<!-- 输入框 -->
		<user-chat-bottom @sendMsg="sendMsg"></user-chat-bottom>
		
		<!-- 分享到 -->
		<more-share :show="isShow" @showmore="showmore"></more-share>
		
	</view>
</template>

<script>
	
	import detailInfo from '../../components/detail/detail-info.vue';
	import timeUtil from '../../common/time.js';
	import commentList from '../../components/detail/comment-list.vue';
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue';
	import moreShare from '../../components/common/more-share.vue';
		
		
	export default {
		components:{
			detailInfo,
			timeUtil,
			commentList,
			userChatBottom,
			moreShare
		},
		data() {
			return {
				isShow:false,
				comment:{
					count:20,
					list:[]
				},
				picitems:{
					userpic: '../../static/demo/userpic/12.jpg',
					username: '哈哈',
					sex: 1, //0 男 1 女
					age: 23,
					isguanzhu: false,
					title: '我是标题',
					titlepic: '../../static/demo/datapic/l5.jpeg',
					morepic:['../../static/demo/datapic/l1.jpeg','../../static/demo/datapic/l2.jpeg','../../static/demo/datapic/l3.jpeg','../../static/demo/datapic/l4.jpeg','../../static/demo/datapic/l1.jpeg','../../static/demo/datapic/l2.jpeg','../../static/demo/datapic/l3.jpeg','../../static/demo/datapic/l4.jpeg'],
					// video:{
					// 	looknum: '20w',
					// 	long: '2:47'
					// },
					share: false,
					path: '深圳 龙岗',
					sharenum: 20,
					commentnum: 30,
					goodnum: 20
					}
			}
		},
		onLoad() {
			// console.log(e);
			// this.initData(JSON.parse(e.detailData))
			this.getcomment();
		},
		// 监听导航栏菜单按钮事件
		onNavigationBarButtonTap(e) {
			if(e.index == 0){
				// console.log("分享");
				this.showmore();
				
			}
		},
		methods: {
			// 发送回复信息
			sendMsg(text){
				let sendData = {
						id:1,
						fid:0,
						userpic:'../../static/demo/datapic/l1.jpeg',
						username:'Fuck_Me_Pls',
						data:text,
						time:timeUtil.gettime.gettime(new Date().getTime())
					}
				this.comment.list.push(sendData);
				// this.scrollToBottom();
				
			},
			// 获取评论信息
			getcomment(){
				let arr = [
					{
						id:1,
						fid:0,
						userpic:'../../static/demo/datapic/l1.jpeg',
						username:'Fuck_Me_Pls',
						data:'特殊时期，我们要特殊对待，抵抗艰苦的日子，将会迎来曙光',
						time:'1583892783'
					},
					{
						id:2,
						fid:1,
						userpic:'../../static/demo/datapic/l2.jpeg',
						username:'let try',
						data:'每天都是好心情看到这个我',
						time:'1583893783'
					},
					{
						id:3,
						fid:1,
						userpic:'../../static/demo/datapic/l3.jpeg',
						username:'科技生活',
						data:'HUAWEI马上要崛起',
						time:'1583894783'
					},
					{
						id:4,
						fid:0,
						userpic:'../../static/demo/datapic/l4.jpeg',
						username:'苍老师',
						data:'退役后，生活越来越滋润了，不想以前拼死拼活的还没有扣饭eating',
						time:'1583895783'
					}
				];
				for (let i = 0; i < arr.length; i++) {
					arr[i].time = timeUtil.gettime.gettime(arr[i].time);
					
				}
				this.comment.list = arr;
				
			},
			initData(obj){
				uni.setNavigationBarTitle({
					title:obj.title
				})
			},
			// 获取当前高度
			scrollToBottom(){
				
				// let q=uni.createSelectorQuery();
				// q.select('#scrollview').boundingClientRect();
				// q.exec(res=>{
				// 	console.log("得到布局位置信息" + JSON.stringify(res));
				// 	console.log("节点离页面顶部的距离为" + res.top);
				// })
				
			},
			showmore(){
				this.isShow = !this.isShow;
			}
			
		},
		mounted(){
			this.scrollToBottom();
		}
	}
</script>

<style>


/* 评论 */
 .u-comment{
	 
	 padding: 0 20upx;
	 
 }
 .u-comment-title{
	 font-size: 30upx;
	 font-weight: bold;
	 padding: 20upx;
 }
 

</style>
