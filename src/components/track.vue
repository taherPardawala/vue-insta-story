<template>
	<div class="track-wrapper">
		{{currentIndex}}
		<div class="track-inner-wrapper">
			<div
				:style="computeStyle"
				v-for="(item, index) in stories.length"
				:key="index"
				class="track-item"
			></div>
		</div>
	</div>
</template>

<script>
	export default {
		name: "Track",
		props: ["currentIndex", "stories"],
		computed: {
			computeStyle() {
				return {
					width: window.innerWidth / this.stories.length
				};
			}
		}
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.track-wrapper {
		.track-inner-wrapper {
			display: flex;
			flex-wrap: nowrap;
			.track-item {
				height: 5px;
				background: #eaeaea;
				// width: 100px;
					margin-left: 1%;
				// &:not(:first-child()) {
				// }
			}
		}
	}
</style>
