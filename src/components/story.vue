<template>
	<div class="story-wrapper">
		<img style="max-width:100%;" :src="stories[currentIndex]" alt />
	</div>
</template>

<script>
	export default {
		name: "Story",
		props: ["stories", "currentIndex"]
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
