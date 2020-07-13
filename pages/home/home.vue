<template>
	<view>
		
		<view class="testcls" :class="{'tstcls2':myindex === 3}" @click="tcl" >
			test
		</view>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				flag:false,
				myindex:2
			}
		},
		methods: {
			tcl(){
				this.flag = !this.flag;
				if(this.myindex == 3){
					this.myindex =2;
				}else{
					this.myindex = 3
				}
				
				
			}
		}
	}
</script>

<style>

.testcls {
	
	height: 100rpx;
	width: 80rpx;
	background-color: #007AFF;
	
}
.tstcls2 {
	
	background-color: #09BB07 !important;
	
}

</style>
