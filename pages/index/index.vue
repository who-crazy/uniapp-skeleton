<template>
	<view class="container">
		<u-navbar title="" :bgColor="bgColor" style="color: #fff;">
			<view class="u-nav-slot" slot="left">
				<view style="font-size: 40rpx;">{{title}}</view>
				<!-- <u-icon @click="$ran.goto('/pages/index/index')" name='home' size='30' color="#0081cd"></u-icon> -->
			</view>
		</u-navbar>
		<view class="u-demo-block__content" style="height: 100%; background-color: #fff; display: flex; flex-direction: column; justify-content: center;">
			<view style="display: flex; justify-content: center; flex-direction: column; align-items: center;">
				<u-grid
				:border="false"
				border
				col="2"
				>
					<u-grid-item
					v-for="(listItem,listIndex) in list"
					:key="listIndex"
					@click="goto(listItem.path)"
					>
						<u--image :src="listItem.img" width="100rpx" height="100rpx" style="margin: 20rpx;"></u--image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
				<!-- <u-toast ref="uToast" /> -->
						
						
				<!-- <view class="nav-list random-number" @click="goto('/pages/index/random')">
					Number
				</view>
				<view class="nav-list" @click="goto('/pages/index/dice')">
					Dice
				</view> -->
			</view>
			
			<!-- <view class="nav-list" @click="goto('/pages/index/coin')">
				Coin
			</view>
			<view class="nav-list" @click="goto('/pages/index/guess')">
				Mora
			</view> -->
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
				title: APP_NAME,
				bgColor: "#3c9cff",//0081cd	//#3c9cff
				list: [
					{
						img: '../../static/random/rd.png',
						path: '/pages/index/random',
						title: 'Number'
					},
					{
						img: '../../static/dice/dice1.png',
						path: '/pages/index/dice',
						title: 'Dice'
					},
					{
						img: '../../static/coin/xingxing.png',
						path: '/pages/index/coin',
						title: 'Coin'
					},
					{
						img: '../../static/guess/jd.png',
						path: '/pages/index/guess',
						title: 'Mora'
					}
				],
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
			goto(router) {
				uni.navigateTo({
					url: router
				})
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
.nav-list{
	width: 50%;
	padding: 25px 60px;
	background-color: #3c9cff;
	border-radius: 5px;
	margin-bottom: 10px;
	color: #fff;
}
.random-number{
	background-image: url('../../static/random/rd.png');
	background-position: right bottom;
	background-repeat: no-repeat;
	background-size: cover;
	/* filter: grayscale(100%) */
}
.grid-text {
	font-size: 14px;
	color: #909399;
	padding: 10rpx 0 20rpx 0rpx;
	/* #ifndef APP-PLUS */
	box-sizing: border-box;
	/* #endif */
}
</style>
