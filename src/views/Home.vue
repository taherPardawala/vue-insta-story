<template>
	<div class="home">
		<Track :stories="stories" :currentIndex="currentIndex" />
		<story :stories="stories" :currentIndex="currentIndex" />
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
					"https://i.imgur.com/T4jwXEX.png",
					"https://i.imgur.com/AY5z4ZP.jpg",
					"https://i.imgur.com/HJBbtOI.jpg",
					"https://i.imgur.com/tXgQukC.jpg"
				],
				currentIndex: 0
			};
		},
		mounted() {
			setInterval(_ => {
				this.currentIndex++;
				if (this.currentIndex === this.stories.length) {
					this.currentIndex = 0;
				}
			}, 1000);
		},
		components: {
			Story,
			Track
		}
	};
</script>
