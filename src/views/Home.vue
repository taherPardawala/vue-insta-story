<template>
	<div class="home">
		<!-- <button @click="show = !show">CLICK</button> -->
		<Track v-if="show" @nextSlide="nextSlide" :stories="stories" :currentIndex="currentIndex" />
		<story
			v-if="show"
			@nextSlide="nextSlide"
			@previousSlide="previousSlide"
			:stories="stories"
			:currentIndex="currentIndex"
		/>
	</div>
</template>

<script>
	// @ is an alias to /src
	import Story from "@/components/story";
	import Track from "@/components/track";

	export default {
		name: "home",
		data: () => {
			return {
				stories: [
					{
						mediaURL: "https://i.imgur.com/T4jwXEX.png",
						type: "image",
						duration: 2000
					},
					{
						mediaURL: "https://i.imgur.com/AY5z4ZP.jpg",
						type: "image",
						duration: 2000
					},
					{
						mediaURL: "https://i.imgur.com/HJBbtOI.jpg",
						type: "image",
						duration: 2000
					},
					{
						mediaURL: "https://i.imgur.com/tXgQukC.jpg",
						type: "image",
						duration: 2000
					},
					{
						mediaURL: require("../assets/coverr-soap-bubbles-outdoor-1567244523991.mp4"),
						type: "video",
						duration: 28000
					}
				],
				currentIndex: 0,
				show: true
			};
		},
		mounted() {},
		methods: {
			nextSlide() {
				if (this.currentIndex === this.stories.length - 1) {
					this.currentIndex = 0;
				} else {
					this.currentIndex++;
				}
			},
			previousSlide() {
				if (this.currentIndex !== 0) {
					this.currentIndex--;
				}
			}
		},
		components: {
			Story,
			Track
		}
	};
</script>

<style lang="scss" scoped>
	.home {
		max-width: 320px;
		.track-wrapper {
			position: absolute;
			top: 2%;
		}
	}
</style>