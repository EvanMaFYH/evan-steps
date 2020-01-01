<template>
	<view class="evan-step-show">
		<view class="evan-step-show__title">
			<text class="evan-step-show__title__item">基础用法</text>
		</view>
		<evan-steps :active="1">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="详情详情详情详情"></evan-step>
			<evan-step title="第三步" description="详情详情详情详情"></evan-step>
		</evan-steps>
		
		<view class="evan-step-show__title">
			<text class="evan-step-show__title__item">自定义主题色</text>
		</view>
		
		<evan-steps :active="1" primaryColor="green">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="详情详情详情详情"></evan-step>
			<evan-step title="第三步" description="详情详情详情详情"></evan-step>
		</evan-steps>
		
		<view class="evan-step-show__title">
			<text class="evan-step-show__title__item">自定义status</text>
		</view>
		
		<evan-steps :active="1">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" status="error" description="详情详情详情详情"></evan-step>
			<evan-step title="第三步" description="详情详情详情详情"></evan-step>
		</evan-steps>
		
		<view class="evan-step-show__title">
			<text class="evan-step-show__title__item">自定义icon</text>
		</view>
		
		<evan-steps :active="1">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="详情详情详情详情"></evan-step>
			<evan-step title="第三步" description="详情详情详情详情"></evan-step>
			<evan-step icon="home" title="自定义icon(来自uni-icons)" description="详情详情详情详情"></evan-step>
			<evan-step title="完全自定义icon" description="详情详情详情详情">
				<template v-slot:icon>
					<evan-icons type="telegram" size="22" color="#ccc"></evan-icons>
				</template>
			</evan-step>
			<evan-step title="完全自定义icon图片" description="详情详情详情详情">
				<template v-slot:icon>
					<image class="evan-step-show__show" src="/static/logo.png"></image>
				</template>
			</evan-step>
		</evan-steps>
		
		<view class="evan-step-show__title">
			<text class="evan-step-show__title__item">水平方向</text>
		</view>

		<evan-steps :active="1" direction="horizontal">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="详情详情详情详情"></evan-step>
			<evan-step icon="home" title="自定义icon" description="详情详情详情详情"></evan-step>
		</evan-steps>
		<!-- #ifdef APP-PLUS -->
		<button @click="goNvue">nvue页面</button>
		<!-- #endif -->
	</view>
</template>

<script>
	import EvanSteps from '@/components/evan-steps/evan-steps.vue'
	import EvanStep from '@/components/evan-steps/evan-step.vue'
	import UniIcons from '@/components/uni-icons/uni-icons.vue'
	import EvanIcons from '@/components/evan-icons/evan-icons.vue'
	export default {
		components: {
			EvanSteps,
			EvanStep,
			UniIcons,
			EvanIcons
		},
		data() {
			return {

			}
		},
		onLoad() {

		},
		methods: {
			goNvue() {
				uni.navigateTo({
					url: '/pages/app/app'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.evan-step-show {
		padding: 20px;
		&__title{
			padding: 10px 0;
			&__item{
				font-size: 16px;
				color: #333;
				font-weight: bold;
			}
		}
		&__show{
			width: 22px;
			height: 22px;
			display: block;
		}
	}
</style>
