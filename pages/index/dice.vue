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
				<view style="display:flex; flex-wrap: wrap; height: 172rpx; width: 60%;">
					<!-- 骰子组件 -->
					<Dice ref="diceRef" v-for="i in diceNum" :key="i" :class="[diceNum == 1 ? 'dice_full' : '', diceNum == 3 && i == 1 ? 'dice_full' : 'dice_default', diceNum == 5 && i == 3 ? 'dice_full' : 'dice_default']"/>
				</view>
			</view>
			
			<view class="">
				<view style="margin-left: 20rpx;">
					<u--text text="Choose Number:" style=""></u--text>
				</view>
				<u-slider v-model="diceNum" min="1" max="6" step="1" blockSize="18" :showValue="true"></u-slider>
			</view>
			<view style="margin-bottom: 20rpx;">
				<u-button type="primary" text="Shake" style='width: 40%;' @click="shake" v-if="!genStatus"></u-button>
				<u-button type="primary" text="Shake..." style='width: 30%;' disabled v-else></u-button>
			</view>
			
		</view>
		
	</view>

</template>

<script>
import { APP_NAME } from '../../config'
	import Dice from "@/components/dice/dice.vue"
	export default {
		components: {
			Dice
		},
		data() {
			return {
				value: '',
				title: 'Dice',
				bgColor: "#3c9cff",//0081cd	//#3c9cff
				//骰子数量
				diceNum: 1,
				genStatus: false,
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
			async shake() {
				this.genStatus = true
				// console.log(this.$refs.diceRef)
				await this.shakeAll()
				this.genStatus = false
			},
			async shakeAll() {
				const diceRefArr = this.$refs.diceRef
				for (let i = 0; i < this.diceNum; i++) {
					diceRefArr[i].throwDice()
				}
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
.dice_default{
	flex: 0 0 50%; 
	display: flex; 
	justify-content: center;
}
.dice_full{
	flex: 0 0 100%;
	display: flex; 
	justify-content: center;
}
</style>
