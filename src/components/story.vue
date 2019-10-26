<template>
	<div class="story-wrapper">
		<img
			v-if="stories[currentIndex].type === 'image'"
			style="max-width:100%;"
			:src="stories[currentIndex].mediaURL"
			alt
		/>
		<video
			v-if="stories[currentIndex].type === 'video'"
			style="max-width:100%;"
			:src="stories[currentIndex].mediaURL"
			autoplay
		></video>
		<!-- {{currentIndex}} -->
	</div>
</template>

<script>
	import Hammer from "hammerjs";
	export default {
		name: "Story",
		props: ["stories", "currentIndex"],
		mounted() {
			this.timeOutHandler = setTimeout(() => {
				this.$emit("nextSlide");
			}, this.stories[this.currentIndex].duration - 1);

			this.hammer = new Hammer.Manager(this.$el, {
				recognizers: [
					[Hammer.Pan, { direction: Hammer.DIRECTION_HORIZONTAL }],
					[Hammer.Tap],
					[Hammer.Press, { time: 200, threshold: 100 }]
				]
			});

			this.hammer.on("press", () => {
				// this.timeline.pause();
				console.log("pressed");
			});

			this.hammer.on("pressup", () => {
				// this.timeline.play();
				console.log("pressed up tap");
			});

			// Tap on the side to navigate between slides
			this.hammer.on("tap", event => {
				clearTimeout(this.timeOutHandler);
				if (event.center.x > window.innerWidth / 3) {
					// this.nextSlide();
					this.$emit("nextSlide");
					console.log("tapped on the right");
				} else {
					// this.previousSlide();
					this.$emit("previousSlide");
					console.log("tapped on the left");
				}
			});

			// Handle swipe
			this.hammer.on("pan", event => {
				if (event.isFinal) {
					if (event.deltaX < 0) {
						// this.nextStory();
						console.log("swiped right");
					} else if (event.deltaX > 0) {
						// this.previousStory();
						console.log("swiped left");
					}
				}
			});
		},
		data: () => {
			return {
				timeOutHandler: null
			};
		},
		watch: {
			currentIndex(nv, cv) {
				this.timeOutHandler = setTimeout(() => {
					this.$emit("nextSlide");
				}, this.stories[this.currentIndex].duration - 1);
			}
		}
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.story-wrapper {
		width: 320px;
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		background: #000;
	}
</style>
