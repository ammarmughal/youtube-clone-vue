<template>
	<div>
		<ul class="list-group">
			<VideoListItem
				v-for="video in videos"
				:key="video.etag"
				:video="video"
				@videoSelect="onVideoSelect"
			></VideoListItem>
		</ul>
	</div>
</template>

<script>
	import VideoListItem from "./VideoListItem";

	export default {
		name: "VideoList",
		props: ["videos"],
		components: {
			VideoListItem
		},
		methods: {
			onVideoSelect(video) {
				this.$emit("videoSelect", video);
			}
		}
	};
</script>

<style scoped>
</style>