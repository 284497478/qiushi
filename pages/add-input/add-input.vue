<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar left-icon="arrowleft" statusBar="true" rightText="发布" @clickLeft="back" @clickRight="submit">
			<view class="u-f-ajc" @tap="changebook">
				{{ yinsi }}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!-- 文本框 -->
		<view class="uni-textarea"><textarea v-model="text" placeholder="说一句话吧~" /></view>
		<!-- 上传多图 -->
		<upload-image @uploadImg="uploadImg"></upload-image>
		
		<!-- 弹出框 -->
		<uni-popup ref="showpopup">
			<view class="addInputPopup">
				<view class="u-f-ajc">
					<image src="../../static/common/unipopup.png" mode="widthFix" />
				</view>
				<view>1、涉及黄色，政治，广告及骚扰信息</view>
				<view>2、涉及人身攻击</view>
				<view>3、留联系方式，透露他人隐私</view>
				<view>一经核实将被封禁，情节严重者永久封禁</view>
				<button type="default" @tap="closePopup">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue';
import uploadImage from '../../components/common/upload-image.vue';
import uniPopup from '../../components/uni-popup/uni-popup.vue';

let changebookArr = ['所有人都可见', '仅自己可见'];
export default {
	components: {
		uniNavBar,
		uploadImage,
		uniPopup
	},
	data() {
		return {
			isget:false,
			yinsi: '所有人都可见',
			text: '',
			imgList:[]
		};
	},
	onLoad() {
	},
	created() {
		this.$nextTick(() => {
			console.log(this.$refs.showpopup);
			this.$refs.showpopup.open();
			console.log("excet");
		})
	},
	onBackPress() {
			
		if(!this.text && this.imgList.length<1) {return ;}
		if(!this.isget){
			this.saveinfo();
			return true;
		}
		
	},
	methods: {
		// 提示保存信息
		saveinfo(){
			uni.showModal({
				title: '提示',
				content: '是否保存已编写内容？',
				cancelText: '不保存',
				confirmText: '保存',
				success: res => {
					if(res.confirm){
						console.log("保存信息");
					}else{
						console.log("不保存信息！");
					}
					this.isget = true;
					uni.navigateBack({
						delta:1
					})
					
				},
			});	
		},
		//返回
		back() {
			uni.navigateBack({
				delta: 1
			});
		},
		// 选择仅自己可见或者所有人
		changebook() {
			uni.showActionSheet({
				itemList: changebookArr,
				success: res => {
					this.yinsi = changebookArr[res.tapIndex];
				}
			});
		},
		// 发布
		submit() {
			console.log('点击了发布。。');
		},
		// 上传图片
		uploadImg(imgList){
			this.imgList = imgList;
			console.log(this.imgList);
			
		},
		// 关闭公告提示
		closePopup(){
			this.$nextTick(() => {
				console.log(this.$refs.showpopup);
				this.$refs.showpopup.close();
				console.log("excut close" );
			})
		}
	}
};
</script>

<style>
.uni-textarea {
	border: 1upx solid #eeeeee;
}
.addInputPopup {
	background-color: #FFFFFF;
	padding: 40upx;
	border-radius: 20upx;
	width: 500upx;
}
.addInputPopup image {
	width: 70%;
	padding-bottom: 20upx;
	
	
}

.addInputPopup button{
	background-color: #FFE934;
	margin-top: 20upx;
	
}
</style>
