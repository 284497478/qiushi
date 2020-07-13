<template>
	<view class="animated fadeIn faster" v-if="show" @click="showmore">
		<view class="more-share-model"></view>
		<view class="more-share">
			<view class="more-share-title u-f-ajc">分享到</view>
			<scroll-view scroll-x class="more-share-body">
				<block v-for="(val ,index) in providerList" :key="index">
					<view class="more-share-item u-f-ajc"  hover-class="more-share-hover" @click="share(val)">
						<view class="icon iconfont u-f-ajc" 
						:class="['icon-'+val.zicon,'more-share-'+val.zclass]">
						</view>
						<view>{{val.name}}</view>
					</view>
				</block>
				<!-- mytestgit -->
				<!-- <view class="more-share-item u-f-ajc"  hover-class="more-share-hover">
					<view class="icon iconfont u-f-ajc icon-pengyouquan more-share-pyq"></view>
					<view>朋友圈</view>
				</view>
				<view class="more-share-item u-f-ajc"  hover-class="more-share-hover">
					<view class="icon iconfont u-f-ajc icon-xinlangweibo more-share-wb"></view>
					<view>微博</view>
				</view>
				<view class="more-share-item u-f-ajc"  hover-class="more-share-hover">
					<view class="icon iconfont icon-QQ u-f-ajc more-share-qq"></view>
					<view>QQ好友</view>
				</view>
				<view class="more-share-item u-f-ajc" hover-class="more-share-hover">
					<view class="icon iconfont icon-weixin u-f-ajc more-share-qq"></view>
					<view>其他</view>
				</view> -->
			</scroll-view>
			<view class="more-share-bottom u-f-ajc" hover-class="more-share-hover">取消</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			show:Boolean
		},
		data() {
			return {
				title: '分享精彩生活',
				shareText: '每一天与你同在',
				href:"https://uniapp.dcloud.io",
				image: '../../static/demo/datapic/l1.jpeg',
				shareType:1,//0，微信好友，1微信朋友圈，2微博，3QQ
				providerList: [{
									name: '微信好友',
									id: 'weixin',
									zicon:'weixin',
									zclass:'wx',
									sort:0
								}]
			}
		},
		onLoad() {
			console.log("onload");
			uni.getProvider({
				service: 'share',
				success: (e) => {
					console.log('success', e);
					let data = []
					for (let i = 0; i < e.provider.length; i++) {
						switch (e.provider[i]) {
							case 'weixin':
								data.push({
									name: '微信好友',
									id: 'weixin',
									zicon:'weixin',
									zclass:'wx',
									sort:0
								})
								data.push({
									name: '朋友圈',
									id: 'weixin',
									type:'WXSenceTimeline',
									zicon:'pengyouquan',
									zclass:'pyq',
									sort:1
								})
								break;
							case 'sinaweibo':
								data.push({
									name: '新浪微博',
									id: 'sinaweibo',
									zicon:'xinlangweibo',
									zclass:'wb',
									sort:2
								})
								break;
							case 'qq':
								data.push({
									name: 'QQ好友',
									id: 'qq',
									zicon:'QQ',
									zclass:'qq',
									sort:3
								})
								break;
							default:
								break;
						}
					}
					this.providerList = data.sort((x,y) => {
						return x.sort - y.sort
					});
					console.log("初始化数据");
					console.log(this.providerList);
				},
				fail: (e) => {
					console.log('获取分享通道失败', e);
					uni.showModal({
						content:'获取分享通道失败',
						showCancel:false
					})
				}
			});
		},
		methods:{
			showmore(){
				this.$emit('showmore');
				this.show = !this.show;
			},
			async share(e) {
				console.log('分享通道:'+ e.id +'； 分享类型:' + this.shareType);
				
				if(!this.shareText && (this.shareType === 1 || this.shareType === 0)){
					uni.showModal({
						content:'分享内容不能为空',
						showCancel:false
					})
					return;
				}
				
				if(!this.image && (this.shareType === 2 || this.shareType === 0)){
					uni.showModal({
						content:'分享图片不能为空',
						showCancel:false
					})
					return;
				}
				
				let shareOPtions = {
					provider: e.id,
					scene: e.type && e.type === 'WXSenceTimeline' ? 'WXSenceTimeline' : 'WXSceneSession', //WXSceneSession”分享到聊天界面，“WXSenceTimeline”分享到朋友圈，“WXSceneFavorite”分享到微信收藏     
					type: this.shareType,
					success: (e) => {
						console.log('success', e);
						uni.showModal({
							content: '已分享',
							showCancel:false
						})
					},
					fail: (e) => {
						console.log('fail', e)
						uni.showModal({
							content: e.errMsg,
							showCancel:false
						})
					},
					complete:function(){
						console.log('分享操作结束!')
					}
				}
				
				switch (this.shareType){
					case 0:
						shareOPtions.summary = this.shareText;
						shareOPtions.imageUrl = this.image;
						shareOPtions.title = '欢迎体验uniapp';
						shareOPtions.href = 'https://uniapp.dcloud.io';
						break;
					case 1:
						shareOPtions.summary = this.shareText;
						break;
					case 2:
						shareOPtions.imageUrl = this.image;
						break;
					case 5:
						shareOPtions.imageUrl = this.image ? this.image : 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/app/share-logo@3.png'
						shareOPtions.title = '欢迎体验uniapp';
						shareOPtions.miniProgram = {
							id:'gh_33446d7f7a26',
							path:'/pages/tabBar/component/component',
							webUrl:'https://uniapp.dcloud.io',
							type:0
						};
						break;
					default:
						break;
				}
				
				if(shareOPtions.type === 0 && plus.os.name === 'iOS'){//如果是图文分享，且是ios平台，则压缩图片 
					shareOPtions.imageUrl = await this.compress();
				}
				if(shareOPtions.type === 1 && shareOPtions.provider === 'qq'){//如果是分享文字到qq，则必须加上href和title
					shareOPtions.href = 'https://uniapp.dcloud.io';
					shareOPtions.title = '欢迎体验uniapp';
				}
				uni.share(shareOPtions);
			},
			radioChange(e){
				console.log('type:' + e.detail.value);
				this.shareType = parseInt(e.detail.value);
			},
			chooseImage() {
				uni.chooseImage({
					count: 1,
					sourceType: ['album', 'camera'],
					sizeType: ['compressed', 'original'],
					success: (res) => {
						this.image = res.tempFilePaths[0];
					},
					fail: (err) => {
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			compress(){//压缩图片 图文分享要求分享图片大小不能超过20Kb
				console.log('开始压缩');
				let img = this.image;
				return new Promise((res) => {
					var localPath = plus.io.convertAbsoluteFileSystem(img.replace('file://', ''));
					console.log('after' + localPath);
					// 压缩size
					plus.io.resolveLocalFileSystemURL(localPath, (entry) => {
						entry.file((file) => {// 可通过entry对象操作图片 
							console.log('getFile:' + JSON.stringify(file));
							if(file.size > 20480) {// 压缩后size 大于20Kb
								plus.zip.compressImage({
									src: img,
									dst: img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG'),
									width: '10%',
									height: '10%',
									quality: 1,
									overwrite: true
								}, (event) => {
									console.log('success zip****' + event.size);
									let newImg = img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG');
									res(newImg);
								}, function(error) {
									uni.showModal({
										content:'分享图片太大,需要请重新选择图片!',
										showCancel:false
									})
								});
							}
						});
					}, (e) => {
						console.log('Resolve file URL failed: ' + e.message);
						uni.showModal({
							content:'分享图片太大,需要请重新选择图片!',
							showCancel:false
						})
					});
				})
			}
			
		}
	}
</script>

<style scoped>
	/* 分享 */
	
	.more-share-model {
		
		background-color: rgba(51, 51, 51, 0.36);
		z-index: 100;
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
			
	}
	
	
	.more-share {
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: #FFFFFF;
		z-index: 101;
	}
	
	.more-share-title,.more-share-bottom {
		font-size: 32upx;
		color: #000000;
		padding: 20upx 0;
		
	}
	
	.more-share-body{
		display: flex;
		white-space: nowrap;
		align-items: center;
		justify-content: center; 
		line-height: 100upx;
		width: 100%;
		border-bottom: 1upx solid #EEEEEE;
	}
	
	.more-share-item {
		width: 25%;
		display: inline-flex;
		flex-direction: column;
		height: 100%;
		
		
	}
	
	.more-share-item>view:first-child {
		
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		font-size: 60upx;
		color: #FFFFFF;
		
	}
	
	.more-share-item>view:last-child {
		
		font-size: 30upx ;
		color: #c3c3c3;
		
	}
	
	
	
	.more-share-hover{
		background: #EEEEEE;
	}
	
	.more-share-wx{
		background: #2AD19B;
	}
	.more-share-pyq{
		background: #514D4C;
	}
	.more-share-wb{
		background: #EE5E5E;
	}
	.more-share-qq{
		background: #4A73BA;
	}
	
</style>
