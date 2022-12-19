<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <VideoList :videos="videos"></VideoList>
    </div>
</template>

<script>
import axios from "axios";

import SearchBar from "./components/SearchBar.vue";
import VideoList from "./components/VideoList.vue";

export default {
    name: "App",
    components: {
        SearchBar,
        VideoList,
    },
    data() {
        return { videos: [] };
    },
    methods: {
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
