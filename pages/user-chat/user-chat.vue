<template>
	<view>
		<scroll-view id="scrollview" scroll-y="true" :scroll-top="scrollTop" scroll-with-animation="true" 
		:style="{height:chatInfo.contentH+'px'}">
			<!--聊天列表  -->
			<block v-for="(item,index) in list" :key="index">
				<user-chat-list :item="item" :index="index"></user-chat-list>
			</block>
		</scroll-view>
		<!-- 输入框 -->
		<user-chat-bottom @sendMsg="sendMsg"></user-chat-bottom>
	</view>
</template>

<script>
	
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue';
	import timeUtil from '../../common/time.js';
	import userChatList from '../../components/user-chat/user-chat-list.vue';
	export default {
		components:{
			userChatBottom,
			timeUtil,
			userChatList
			
		},
		data() {
			return {
				list:[],
				scrollTop:0,
				chatInfo:{
					contentH:0,
					chatH:0
				}
				
			}
		},
		onLoad() {
		
			this.getData();
			this.initData();
		},
		onReady() {
			
			this.pageToBottom();
		},
		methods: {
			initData(){
				// let bottomH = 0;
				// uni.getSystemInfo({
				//     success: (res)=> {
				// 		// let queryBottom = uni.createSelectorQuery();
				// 		// queryBottom.select('.user-chat-bottom').boundingClientRect(data => {
				// 		//   bottomH = data.height;
				// 		  // this.chatInfo.contentH =  res.windowHeight - bottomH ;
				// 		  this.chatInfo.contentH =  res.windowHeight - uni.upx2px(120) ;
				// 		  // console.log(this.chatInfo.contentH);
				// 		  // console.log(uni.upx2px(120));
				// 		  // console.log(res.windowHeight);
				// 		  // console.log(res.screenHeight);
				// 		// }).exec();
				//     }
				// });
				try {
					const res = uni.getSystemInfoSync();
					this.chatInfo.contentH=res.windowHeight - uni.upx2px(120);
				} catch (e) { }
			},
			pageToBottom(){
				// let queryList = uni.createSelectorQuery();
				// queryList.select('#scrollview').boundingClientRect();
				// queryList.selectAll('.user-chat-list').boundingClientRect(data =>{
				// 	console.log(JSON.stringify(data));
				// data.forEach(res=>{
					
				// 	console.log(res.height);
				// 	this.chatInfo.chatH += res.height;
				// 	if(this.chatInfo.chatH > this.chatInfo.contentH){
				// 		this.scrollTop = this.chatInfo.chatH;
				// 	}
				// 	console.log(this.scrollTop + " : "+ this.chatInfo.contentH);
				// })
					
				// }).exec();
				
				let q=uni.createSelectorQuery();
				q.select('#scrollview').boundingClientRect();
				q.selectAll('.user-chat-item').boundingClientRect();
				
				q.exec((res)=>{
					
					res[1].forEach((ret)=>{
						
						this.chatInfo.chatH += ret.height;
						
						// console.log(ret.height);
						// console.log(this.chatInfo.chatH);
					});
					setTimeout(() => {
						if(this.chatInfo.chatH > this.chatInfo.contentH){
							this.scrollTop=this.chatInfo.chatH;
						}
					}, 100)
						// console.log(this.scrollTop);
				})
				
				
				
				
			},
			sendMsg(text){
				
				let now = new Date().getTime();
				let info={
						isme:true,
						userpic:"../../static/demo/datapic/lvyou4.jpeg",
						type:"text",
						data:text,
						time:now,
						gstime:timeUtil.gettime.getChatTime(now,this.list[this.list.length-1].time)
					}
			
				this.list.push(info);
				this.pageToBottom();
			},
			getData(){
				
				let arr = [
					{
						isme:false,
						userpic:"../../static/demo/datapic/lvyou3.jpeg",
						type:"text",
						data:"终身学习，用好大脑1",
						time:"158260946"
						
					},
					{
						isme:true,
						userpic:"../../static/demo/datapic/lvyou4.jpeg",
						type:"img",
						data:"../../static/demo/datapic/lvyou3.jpeg",
						time:"158261146"
						
					},
				];
				
				for (var i = 0; i < arr.length; i++) {
					arr[i].gstime = timeUtil.gettime.getChatTime(arr[i].time,i > 0 ?arr[i-1].time :0);
				}
				this.list = arr;
				
			}
		}
	}
</script>

<style>
	
</style>
