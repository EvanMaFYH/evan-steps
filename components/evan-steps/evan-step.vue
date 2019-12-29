<template>
	<view class="evan-step" :class="'evan-step--'+direction">
		<view v-if="customizeIcon" class="evan-step__icon-wrapper" :class="'evan-step__icon-wrapper--'+direction">
			<slot name="icon"></slot>
		</view>
		<view class="evan-step__icon-wrapper" :class="'evan-step__icon-wrapper--'+direction" v-else-if="icon">
			<uni-icons :type="icon" size="22" :color="customIconColor" class="evan-step__custom-icon" :class="'evan-step__custom-icon--'+direction"></uni-icons>
		</view>
		<view v-else class="evan-step__circle" :class="['evan-step__circle--'+direction,'evan-step__circle--'+currentStatus]"
		 :style="{borderColor:circleStyle.borderColor,backgroundColor:circleStyle.backgroundColor,color:circleStyle.color}">
			<uni-icons v-if="currentStatus==='finish'" type="checkmarkempty" :color="primaryColor" size="18"></uni-icons>
			<uni-icons v-else-if="currentStatus==='error'" type="closeempty" color="#fff" size="18"></uni-icons>
			<text class="evan-step__circle__text" :class="'evan-step__circle__text--'+currentStatus" v-else>{{index+1}}</text>
		</view>
		<view class="evan-step__content" :class="'evan-step__content--'+direction">
			<text class="evan-step__content__title" :class="'evan-step__content__title--'+direction" :style="{color:titleColor}">{{title}}</text>
			<text class="evan-step__content__description" :class="'evan-step__content__description--'+direction" :style="{color:descriptionColor}">{{description}}</text>
		</view>
		<view class="evan-step__line" :class="'evan-step__line--'+direction" v-if="!isLast">
			<view :class="'evan-step__line--'+direction+'__inner'" :style="{backgroundColor:lineColor}"></view>
		</view>
	</view>
</template>

<script>
	import UniIcons from '@/components/uni-icons/uni-icons.vue'
	export default {
		name: 'EvanStep',
		components: {
			UniIcons
		},
		props: {
			title: {
				type: String,
				default: ''
			},
			description: {
				type: String,
				default: ''
			},
			// wait process finish error success
			status: {
				type: String,
				default: ''
			},
			icon: {
				type: String,
				default: ''
			}
		},
		computed: {
			direction() {
				const parent = this.getParent()
				return parent.direction
			},
			activeIndex() {
				const parent = this.getParent()
				return parent.active
			},
			primaryColor() {
				const parent = this.getParent()
				return parent.primaryColor
			},
			errorColor() {
				const parent = this.getParent()
				return parent.errorColor
			},
			isLast() {
				if (this.index === null) {
					return true
				}
				const parent = this.getParent()
				return parent.steps.length - 1 === this.index
			},
			currentStatus() {
				if (this.status) {
					return this.status
				}
				const parent = this.getParent()
				const active = parent.active
				if (this.index < active) {
					return 'finish'
				} else if (this.index === active) {
					return 'process'
				} else {
					return 'wait'
				}
			},
			nextStatus() {
				const parent = this.getParent()
				const steps = parent.steps
				if (this.index === steps.length - 1) {
					return ''
				}
				const nextIndex = this.index + 1
				if (steps && steps[nextIndex] && steps[nextIndex].status) {
					return steps[nextIndex].status
				}
				const active = parent.active
				if (nextIndex < active) {
					return 'finish'
				} else if (nextIndex === active) {
					return 'process'
				} else {
					return 'wait'
				}
			},
			circleStyle() {
				switch (this.currentStatus) {
					case 'finish':
						return {
							backgroundColor: '#fff',
							borderColor: this.primaryColor,
							color: this.primaryColor
						}
					case 'process':
						return {
							backgroundColor: this.primaryColor,
							borderColor: this.primaryColor,
							color: '#fff'
						}
					case 'wait':
						return {
							backgroundColor: '#ccc',
							borderColor: '#ccc',
							color: '#fff'
						}
					case 'error':
						return {
							backgroundColor: this.errorColor,
							borderColor: this.errorColor,
							color: '#fff'
						}
					default:
						return {
							backgroundColor: '#fff',
							borderColor: this.primaryColor,
							color: this.primaryColor
						}
				}
			},
			titleColor() {
				switch (this.currentStatus) {
					case 'finish':
						return 'rgba(0,0,0,0.65)'
					case 'process':
						return 'rgba(0,0,0,0.85)'
					case 'wait':
						return 'rgba(0,0,0,0.45)'
					case 'error':
						return this.errorColor
					default:
						return 'rgba(0,0,0,0.85)'
				}
			},
			descriptionColor() {
				switch (this.currentStatus) {
					case 'finish':
						return 'rgba(0,0,0,0.45)'
					case 'process':
						return 'rgba(0,0,0,0.65)'
					case 'wait':
						return 'rgba(0,0,0,0.45)'
					case 'error':
						return this.errorColor
					default:
						return 'rgba(0,0,0,0.85)'
				}
			},
			customIconColor() {
				switch (this.currentStatus) {
					case 'finish':
						return this.primaryColor
					case 'process':
						return this.primaryColor
					case 'wait':
						return '#ccc'
					case 'error':
						return this.errorColor
					default:
						return this.primaryColor
				}
			},
			lineColor() {
				switch (this.nextStatus) {
					case 'finish':
						return this.primaryColor
					case 'process':
						return this.primaryColor
					case 'wait':
						return '#ddd'
					case 'error':
						return this.errorColor
					default:
						return this.primaryColor
				}
			}
		},
		data() {
			return {
				index: null,
				customizeIcon: false
			}
		},
		methods: {
			getParent() {
				// // #ifdef H5
				// return this.$parent.$options.parent
				// // #endif
				// // #ifndef H5
				// return this.$parent
				// // #endif
				let parent = this.$parent
				let parentName = parent.$options.name
				while (parentName !== 'EvanSteps') {
					parent = parent.$parent
					parentName = parent.$options.name
				}
				return parent
			}
		},
		mounted() {
			this.customizeIcon = this.$scopedSlots.icon || false
			const parent = this.getParent()
			this.index = parent.steps.length
			parent.steps.push({
				title: this.title,
				description: this.description,
				status: this.status
			})
		}
	}
</script>

<style lang="scss">
	.evan-step {
		position: relative;
	}

	.evan-step--vertical {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
	}

	.evan-step--horizontal {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		flex: 1;
	}

	.evan-step__icon-wrapper {
		width: 22px;
		height: 22px;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.evan-step__icon-wrapper--vertical {
		margin-right: 8px;
	}

	.evan-step__icon-wrapper--horizontal {
		margin-left: 39px;
	}

	.evan-step__line {
		/* #ifndef APP-NVUE */
		box-sizing: border-box;
		/* #endif */
	}

	.evan-step__line--vertical {
		position: absolute;
		width: 22px;
		height: 100%;
		top: 0;
		left: 0;
		padding: 28px 0 6px 0;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
	}

	.evan-step__line--vertical__inner {
		width: 1px;
		height: 100%;
	}

	.evan-step__line--horizontal {
		position: absolute;
		width: 100%;
		height: 22px;
		top: 0;
		left: 39px;
		padding: 0 6px 0 28px;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		align-items: center;
	}

	.evan-step__line--horizontal__inner {
		width: 100%;
		height: 1px;
	}

	.evan-step__circle {
		width: 22px;
		height: 22px;
		border-radius: 11px;
		border-color: #fff;
		border-width: 1px;
		border-style: solid;
		background-color: #fff;
		/* #ifndef APP-NVUE */
		display: flex;
		box-sizing: border-box;
		/* #endif */
		align-items: center;
		justify-content: center;
	}

	.evan-step__circle--vertical {
		margin-right: 8px;
	}

	.evan-step__circle--horizontal {
		margin-left: 39px;
	}

	.evan-step__circle--finish {}

	.evan-step__circle--process {}

	.evan-step__circle--wait {}

	.evan-step__circle__text {
		font-size: 14px;
	}

	.evan-step__circle__text--process {
		color: #fff;
	}

	.evan-step__content {
		/* #ifndef APP-NVUE */
		display: flex;
		word-break: break-all;
		/* #endif */
		flex-direction: column;
	}

	.evan-step__content--horizontal {
		width: 100px;
		margin-top: 8px;
	}

	.evan-step__content--vertical {
		flex: 1;
	}

	.evan-step__content__title {
		font-size: 16px;
		margin-bottom: 3px;
		font-weight: 500;
	}

	.evan-step__content__title--horizontal {
		text-align: center;
	}

	.evan-step__content__title--vertical {
		width: 100%;
	}

	.evan-step__content__description {
		font-size: 12px;
	}

	.evan-step__content__description--vertical {
		padding-bottom: 12px;
		width: 100%;
	}

	.evan-step__content__description--horizontal {
		text-align: center;
	}
</style>
