<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail :video="selectedVideo"></VideoDetail>
            <VideoList
                @videoSelect="onVideoSelect"
                :videos="videos"
            ></VideoList>
        </div>
    </div>
</template>

<script>
import axios from "axios";

import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";
import VideoDetail from "./components/VideoDetail";

export default {
    name: "App",
    components: {
        SearchBar,
        VideoList,
        VideoDetail,
    },
    data() {
        return { videos: [], selectedVideo: null };
    },
    methods: {
        onVideoSelect(video) {
            this.selectedVideo = video;
        },
        onTermChange(searchTerm) {
            axios
                .get("https://www.googleapis.com/youtube/v3/search", {
                    params: {
                        key: "",
                        type: "video",
                        part: "snippet",
                        q: searchTerm,
                    },
                })
                .then((response) => {
                    this.videos = response.data.items;
                });
        },
    },
};
</script>
