<template>
	<view class="">
		<uni-nav-bar fixed="true" statusBar="true" @clickRight="addOpen" class="nav-bar">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-bar-left u-f-ajc"><view class="icon iconfont icon-qiandao"></view></view>
			</block>
			<!-- 中间 -->
			<block v-for="(news, index) in newsItems" :key="news.id">
				<view class="nav-bar-center u-f-ajc" @click="changeItem(index)">
					<view :class="{ isActive: currentIndex == index }">
						{{ news.newItem }}
						<view class="nav-bar-center-line"></view>
					</view>
				</view>
			</block>
			<!-- 右边 -->
			<block slot="right">
				<view class="nav-bar-right"><view class="icon iconfont icon-bianji1"></view></view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue';

export default {
	components: {
		uniNavBar
	},
	props:{
		newsItems: Array,
		currentIndex: Number
	},
	data() {
		return {
			
		};
	},
	methods: {
		changeItem(currentIndex) {
			this.$emit('change-item', currentIndex);
		},
		addOpen() {
			uni.navigateTo({
				url: '../add-input/add-input'
			});
		}
	}
};
</script>

<style scoped>
.nav-bar-left {
	color: #ff950c;
	width: 60upx;
}
.nav-bar-left > view,
.nav-bar-right > view {
	font-size: 42upx;
}
.nav-bar-right {
	width: 60upx;
	display: flex;
	justify-content: flex-end;
	align-items: center;
	position: relative;
	right: -18upx;
}
.nav-bar-center > view {
	padding: 0 15upx;
	font-weight: bold;
	font-size: 30upx;
	color: #969696;
	height: 50upx;
}
.isActive .nav-bar-center-line {
	border-bottom: 5upx solid #fede33;
	width: 65upx;
	border-top: 5upx solid #fede33;
	border-radius: 10upx;
	margin: auto;
	position: relative;
	bottom: 5upx;
}
.nav-bar-center .isActive {
	color: #000000;
}
</style>
