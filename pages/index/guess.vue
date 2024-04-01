<template>
	<view class="container">
		<u-navbar title="" :bgColor="bgColor" style="color: #fff;">
			<view class="u-nav-slot" slot="left" style="display: flex; align-items: center;">
				<u-icon @click="$ran.goto('/pages/index/index')" name='arrow-leftward' size='20' color="#fff" style="margin-right: 20rpx;"></u-icon>
				<view style="font-size: 40rpx;">{{title}}</view>
			</view>
		</u-navbar>
		<view class="u-demo-block__content" style="height: 100%; background-color: #fff; display: flex; flex-direction: column; justify-content: center;">
			<view style="flex-grow: 1.5;"></view>
			<view style="flex-grow: 3; display: flex; justify-content: center;">
				<u--image :src="imgs[randomNum-1]" mode="aspectFit"></u--image>
			</view>
			
			<view style="margin-bottom: 20rpx;">
				<u-button type="primary" text="Play" style='width: 40%;' @click="play" v-if="!genStatus"></u-button>
				<u-button type="primary" text="Play..." style='width: 30%;' disabled v-else></u-button>
			</view>
		</view>
	</view>

</template>

<script>
import { APP_NAME } from '../../config'
	export default {
		components: {
		},
		data() {
			return {
				value: '',
				title: 'Mora',
				bgColor: "#3c9cff",//0081cd	//#3c9cff
				genStatus: false,
				startValue: 1,
				endValue: 3,
				randomNum: 1,
				imgs: [
					'/static/guess/jd.png',
					'/static/guess/st.png',
					'/static/guess/bu.png'
				]
			}
		},
		onPageScroll(e) {
		},
		onReachBottom() {
		},
		onLoad() {
			
		},
		beforeDestroy() {
			
		},
		methods: {
			play() {
				this.genStatus = true
				let count = 0
				var genInterval = setInterval(() => {
				  this.randomNum = Math.floor(Math.random() * (this.endValue - this.startValue + 1)) + this.startValue; 
				  count++
				  if (count > 20) {
					clearInterval(genInterval)
					this.genStatus = false
				  }
				}, 50)
			}
		},
		mounted: function(){
		}
	}
</script>
<style>
.container{
	display: flex;
	flex-direction: column;
	height: 100%;
}
</style>
