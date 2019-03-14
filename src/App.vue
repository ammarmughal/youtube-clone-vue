<template>
	<div class="container">
		<SearchBar @termChange="onTermChange"></SearchBar>
		<VideoDetail :video="selectedVideo"/>
		<VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
	</div>
</template>

<script>
	import axios from "axios";
	import SearchBar from "./components/SearchBar";
	import VideoList from "./components/VideoList";
	import VideoDetail from "./components/VideoDetail";

	const API_KEY = "AIzaSyA8r8piol3N4AkJnt7ydoM6Z26dApHIwgk";

	export default {
		name: "App",
		data() {
			return {
				videos: [],
				selectedVideo: null
			};
		},
		components: {
			SearchBar,
			VideoList,
			VideoDetail
		},
		methods: {
			onVideoSelect(video) {
				this.selectedVideo = video;
			},
			onTermChange(searchTerm) {
				axios
					.get("https://www.googleapis.com/youtube/v3/search", {
						params: {
							key: API_KEY,
							type: "video",
							part: "snippet",
							q: searchTerm
						}
					})
					.then(response => {
						this.videos = response.data.items;
					});
			}
		}
	};
</script>

<style scoped>
</style>