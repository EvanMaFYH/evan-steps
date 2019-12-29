<template>
	<view class="evan-step-show">
		<evan-steps :active="2">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="详情详情详情详情"></evan-step>
			<evan-step title="第三步" description="特别长特别长特别长特别长特别长特别长特别长特别长特别长特别长特别长特别长特别长"></evan-step>
			<evan-step icon="home" title="自定义icon(来自uni-icons)" description="3333333"></evan-step>
			<evan-step title="完全自定义icon" description="3333333">
				<template v-slot:icon>
					<evan-icons type="telegram" size="22" color="#ccc"></evan-icons>
				</template>
			</evan-step>
		</evan-steps>

		<evan-steps :active="1" direction="horizontal">
			<evan-step title="第一步" description="详情详情详情详情"></evan-step>
			<evan-step title="第二步" description="特别长"></evan-step>
			<!-- <evan-step title="custom" description="3333333">
				<template v-slot:icon>
					<uni-icons type="home" size="22" color="#ccc"></uni-icons>
				</template>
			</evan-step> -->
			<evan-step icon="home" title="自定义icon" description="horizontal"></evan-step>
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

<style>
	.evan-step-show {
		padding: 20px;
	}
</style>
