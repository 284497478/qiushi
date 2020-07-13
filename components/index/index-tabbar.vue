<template>
	<view>
		<view class="uni-tab-bar">
			<scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
				<block v-for="(tab , index) in tabBars" :key="tab.id">
					<view class="swiper-tab-list" :class="{'myclass':currenTabBarIndex == index}" @tap="ontabtap(index)" :style="scrollItemStyle">
					{{tab.name}} {{tab.num?tab.num :''}}
					<view class="currentCls"></view>
					</view>
				</block>
			</scroll-view>
		</view> 
	</view>
</template>

<script>
	export default {
		
		props:{
			tabBars:Array,
			currenTabBarIndex:Number,
			scrollStyle:{
				type:String,
				default:""
			},
			scrollItemStyle:{
				type:String,
				default:""
			}
		},
		methods:{
			//子组件传递数据回父组件
			ontabtap(index){
				this.$emit('changeTabBarIndex',index);
			}
		}
	}
</script>

<style scoped>
	
	
	.uni-swiper-tab {
		border-bottom: 1upx solid #EEEEEE;
	}	
		
	.swiper-tab-list{
		
		color: #979797;
		font-weight: bold;
	}
	
	.uni-swiper-tab .myclass{
		color: #343434;
	}
	.myclass .currentCls {
		border-bottom: 6upx solid #FEDE33;
		width: 60upx;
		margin: auto;
		border-radius: 40upx;
		border-top: 6upx solid #FEDE33;
	}
	

</style>
