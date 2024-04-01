<template>
	<view class="container">
		<u-navbar title="" :bgColor="bgColor" style="color: #fff;" :autoBack='true'>
			<view class="u-nav-slot" slot="left" style="display: flex; align-items: center;">
				<u-icon @click="$ran.goto('/pages/index/index')" name='arrow-leftward' size='20' color="#fff" style="margin-right: 20rpx;"></u-icon>
				<view style="font-size: 40rpx;">{{title}}</view>
			</view>
		</u-navbar>
		<view class="u-demo-block__content" style="height: 100%; background-color: #fff; display: flex; flex-direction: column; justify-content: center;">
			<view style="flex-grow: 1.5;"></view>
			<view style="flex-grow: 3; display: flex; justify-content: center;">
				<!-- coin -->
				<view class="rotate-wrap" :class="[genStatus == true ? (isHeads == true ? 'rotate-wrap-ani-z' : 'rotate-wrap-ani-f') : '']">
					<view class="front circle" :class="[isHeads == true ? 'is-head' : '']"></view>
					<view class="reverse circle" :class="[isHeads == false ? 'is-head' : '']"></view>
				</view>
			</view>
			<view style="margin-bottom: 20rpx;">
				<u-button type="primary" text="Throw" style='width: 40%;' @click="throwCoin" v-if="!genStatus"></u-button>
				<u-button type="primary" text="Throw..." style='width: 40%;' disabled v-else></u-button>
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
				title: 'Coin',
				bgColor: "#3c9cff",//0081cd	//#3c9cff
				genStatus: false,
				isHeads: true,
				endHeads: false
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
			//抛起： 逐渐变大
			//起落过程中前后旋转(先快后慢，降落又快)
			//降落：逐渐变小
			//指定落地方向
			//手动翻面
			throwCoin() {
				this.genStatus = true
				this.isHeads = Math.random() < 0.5;
				setTimeout(() => {
					this.genStatus = false;
				}, 2500); // 休眠5秒，5000毫秒
				
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
.rotate-wrap {
	width: 100px;
	height: 100px;
	margin: 100px;
	transform-style: preserve-3d;
	position: relative;
}
.rotate-wrap-ani-z{
	/* animation: rotate 5s; */
	animation: rotateZ 2.5s linear infinite;
}
.rotate-wrap-ani-f{
	/* animation: rotate 5s; */
	animation: rotateF 2.5s linear infinite;
}
.rotate-wrap:hover {
	animation-play-state: paused;
}
.rotate-wrap .front, .rotate-wrap .reverse{
	width: 100px;
	height: 100px;
	background-size: cover;
}
.rotate-wrap .front{
	position: absolute;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
	background-image: url('../../static/coin/dollar.png');
}
.rotate-wrap .reverse{
	background-image: url('../../static/coin/xingxing.png');
}

.circle{
	border-radius: 50%;
}
.line{
	height: 200px;
	width: 1px;
	position:absolute;
	top: 0;
	left: 50%;
	background: red;
	transform: translateZ(0px);
}
.is-head{
	transform: translateZ(1px);
}

@keyframes rotateZ {
	0%{
		transform: rotateX(0deg);
	}
	20%{
		transform: rotateX(720deg) scale(1.2);
	}
	50%{
		transform: rotateX(1080deg) scale(1.5);
	}
	80%{
		transform: rotateX(1440deg) scale(1.2);
	}
	100% {
		transform: rotateX(2160deg);
	}
}

@keyframes rotateF {
	0%{
		transform: rotateX(0deg);
	}
	20%{
		transform: rotateX(720deg) scale(1.2);
	}
	50%{
		transform: rotateX(1080deg) scale(1.5);
	}
	80%{
		transform: rotateX(1440deg) scale(1.2);
	}
	100% {
		transform: rotateX(1980deg);
	}
}
</style>
