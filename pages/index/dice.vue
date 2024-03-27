<template>
	<view class="container">
		<u-navbar title="" :bgColor="bgColor" style="color: #fff;">
			<view class="u-nav-slot" slot="left">
				{{title}}
				<!-- <u-icon @click="$ran.goto('/pages/index/index')" name='home' size='30' color="#0081cd"></u-icon> -->
			</view>
		</u-navbar>
		<view class="u-demo-block__content" style="height: 100%; background-color: #fff; display: flex; flex-direction: column; justify-content: center;">
			<view style="flex-grow: 2;"></view>
			<view style="flex-grow: 3; display: flex; justify-content: center;">
				<!-- 骰子组件 -->
				<view class="dice-wrap" @tap="throwDice">
					<!-- 筛子运动时候的展示的图片 -->
					<image v-if="isDicing" :src="diceAnimationImages[aniIndex]" class="dice-icon"></image>
					<!-- 筛子静止时候的显示的对应点数的图片 -->
					<image v-else :src="diceImages[currentPoint]" class="dice-icon"></image>
				</view>
			</view>
		</view>
		
	</view>

</template>

<script>
import { APP_NAME } from '../../config'
	// import swiperList from "@/ran-common/data/swiper.js"
	export default {
		data() {
			return {
				value: '',
				title: APP_NAME,
				bgColor: "#3c9cff",//0081cd	//#3c9cff
				//是否正在掷筛子
				isDicing: false,
				//当前显示的动画图片索引
				aniIndex: 0,
				//掷筛子动画所用到的图片(4张骰子旋转过程中的图)
				diceAnimationImages: [
					'/static/dice/dice_run1.png',
					'/static/dice/dice_run2.png',
					'/static/dice/dice_run3.png',
					'/static/dice/dice_run4.png'
				],
				//骰子每一个点的对应的图片
				diceImages: {
					//1点的图片
					1: '/static/dice/dice1.png',
					//2点的图片
					2: '/static/dice/dice2.png',
					//3点的图片
					3: '/static/dice/dice3.png',
					//4点的图片
					4: '/static/dice/dice4.png',
					//5点的图片
					5: '/static/dice/dice5.png',
					//6点的图片
					6: '/static/dice/dice6.png'
				},
				//当前掷筛子掷到的点数（默认1点）
				currentPoint: 1,
				//定时器
				timer: null,
				//骰子数量
				diceNum: 1,
			}
		},
		onPageScroll(e) {
		},
		onReachBottom() {
		},
		onLoad() {
			
		},
		beforeDestroy() {
			//组件销毁之前清除定时器
			clearInterval(this.timer);
		},
		methods: {
			async getDicePoint() {
				let point = 1;
				//从1~6随机一个数
				point = Math.floor(Math.random() * 6 + 1);
				return point;
			},
			//掷骰子
			async throwDice() {
				//如果当前骰子正在滚动则不能掷骰子
				if (this.isDicing) {
					return
				}
				//从接口获取点数
				this.currentPoint = await this.getDicePoint();
				//开启骰子动画
				await this.startAnimation();
				//动画完毕之后可以通知父组件当前掷到的点数
				this.$emit('throwEnd', this.currentPoint);
			},
			//开启动画效果
			async startAnimation() {
				return new Promise((resolve) => {
					//设置筛子开始运动
					this.isDicing = true;
					//记录动画次数
					let num = 0;
					//每隔100毫秒来回切换一张“动”图形成掷骰子的动画
					this.timer = setInterval(() => {
						let index = this.aniIndex;
						index++;
						if (index >= this.diceAnimationImages.length) {
							index = 0;
						}
						this.aniIndex = index;
						num++;
						//差不多执行1.2秒钟的时候可以停止了
						if (num > 12) {
							//关闭定时器
							clearInterval(this.timer);
							//设置骰子停止
							this.isDicing = false;
							//返回结果
							resolve(true);
						}
					}, 100);
				})
			},
		},
		mounted: function(){
		}
	}
</script>
<style>
@keyframes dice-animation {
  0% {
    transform: rotateX(0deg) rotateY(0deg);
  }
  100% {
    transform: rotateX(360deg) rotateY(360deg);
  }
}
.container{
	display: flex;
	flex-direction: column;
	height: 100%;
}
 
.dice-wrap {
	width: 172rpx;
	height: 172rpx;

	.dice-icon {
		width: 172rpx;
		height: 172rpx;
	}
}

</style>
