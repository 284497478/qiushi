<template>
	<view>
		<template v-if="list.length > 0">
			<block v-for="(item, index) in list" :key="index">
				<index-list :item="item" :index="index"></index-list></block>
			<loadMore :loadMoreText="loadMorText"></loadMore>
		</template>
		<template v-else-if="issearch && list.length < 1">
			<nothing></nothing>
		</template>
	</view>
</template>

<script>
import indexList from '../../components/index/index-context.vue';
import nothing from '../../components/common/no-thing.vue';
import loadMore from '../../components/common/load-more.vue';
export default {
	components: {
		indexList,
		nothing,
		loadMore
	},
	data() {
		return {
			times: 3,
			issearch: false,
			loadMorText: '上拉加载更多...',
			list: [],
			searchText:''
		};
	},
	//监听原生标题按钮点击事件（取消按钮）
	onNavigationBarButtonTap(e) {
		if (e.index == 0) {
			uni.navigateBack({
				delta: 1
			});
		}
	},
	//监听原生标题栏搜索输入框输入内容变化事件
	onNavigationBarSearchInputChanged(e) {
		this.searchText = e.text;
		console.log(e.text);
	},
	//监听用户在键盘上点击搜索确认事件
	onNavigationBarSearchInputConfirmed(e) {
		// console.log(e.text);
		if(e.text){
			this.getData();
		}
	},
	// 下拉触底事件
	onReachBottom() {
		this.loadMoreInfo();
	},
	// 下拉刷新
	onPullDownRefresh() {
		
		this.getData();
		uni.stopPullDownRefresh();
	},
	onLoad() {
		this.list = [
			// {
			// 	userPic: '../../static/demo/userpic/6.jpg',
			// 	nickName: 'Allen',
			// 	isFocusOn: false,
			// 	title: '花瓣的美女就是多',
			// 	type: 'img', //img:图文，video：视频
			// 	titlePic: '../../static/demo/datapic/lvyou4.jpeg',
			// 	infoNum: {
			// 		infoType: 0, //0,无操作，1：顶，2：踩
			// 		dingNum: 10,
			// 		caiNum: 13
			// 	},
			// 	commentNum: 12,
			// 	shareNum: 10
			// }
		];
	},
	methods: {
		getData() {
			uni.showLoading({
				title: '小度马上给你惊喜...',
				mask: false
			});
			// 服务器获取数据 传入this.searchText
			let arr = [
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
			];

			setTimeout(() => {
				this.list = arr;
				uni.hideLoading();
				this.issearch = true;
			}, 3000);
		},
		loadMoreInfo() {
			if (this.loadMorText != '上拉加载更多...') {
				return;
			}
			this.loadMorText = '加载中..';
			let loadResult = setTimeout(() => {
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

				this.list.push(tmpObj);

				this.times--;
				if (this.times == 0) {
					this.loadMorText = '没有更多数据了';
				} else {
					this.loadMorText = '上拉加载更多...';
				}
			}, 3000);
		}
	}
};
</script>

<style></style>
