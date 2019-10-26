<template>
	<div class="track-wrapper">
		<div class="track-inner-wrapper">
			<div
				:style="computeStyle"
				v-for="(item, index) in stories.length"
				:key="index"
				class="track-item"
			>
				<div
					:style="index === currentIndex && getComputedTransitionStyle(index)"
					:class="{'track-item-inner': true, 'selected-track-item': index === currentIndex ,['selected-track-item-' + index]: true}"
				></div>
			</div>
		</div>
	</div>
</template>

<script>
	import { watch } from "fs";
	export default {
		name: "Track",
		props: {
			currentIndex: {
				type: Number,
				default: -1
			},
			stories: Array
		},
		created() {},
		mounted() {
			let selectedTrackInnerItem = document.getElementsByClassName(
				"track-item-inner"
			)[0];
			selectedTrackInnerItem &&
				selectedTrackInnerItem.classList.remove("selected-track-item");
			setTimeout(() => {
				selectedTrackInnerItem &&
					selectedTrackInnerItem.classList.add("selected-track-item");
			}, 0);
		},
		data: () => {
			return {};
		},
		computed: {
			computeStyle() {
				return {
					width: 300 / this.stories.length + "px"
				};
			}
		},
		methods: {
			getComputedTransitionStyle(index) {
				let duration = (this.stories[index].duration + 10) / 1000;
				return {
					transition: `width ${duration}s ease-out`
					// transition: `width ${duration}s ease-in-out, visibility ${duration}s linear`
				};
			},
			getComputedSelectedClass(index) {
				return {
					"selected-track-item": true
				};
			}
		},
		watch: {
			currentIndex(nv, cv) {}
		}
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.track-wrapper {
		width: 100%;
		max-width: 320px;
		.track-inner-wrapper {
			display: flex;
			flex-wrap: nowrap;
			justify-content: space-evenly;
			.track-item {
				height: 6px;
				border-radius: 500px;
				background: lightgray;
				box-sizing: border-box;
				&:not(:first-child) {
					margin-left: 1%;
				}

				.track-item-inner {
					width: 0%;
					height: 100%;
				}

				.selected-track-item {
					width: 100%;
					background-color: #fff;
					border-radius: 500px;
				}
			}
		}
	}
</style>
