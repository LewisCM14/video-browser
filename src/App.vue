<template>
    <div>
        <SearchBar @termChange="onTermChange"></SearchBar>
    </div>
</template>
  
<script>
import axios from 'axios'

import SearchBar from './components/SearchBar.vue'
const API_KEY = 'AIzaSyBFGnFsYBM3ZTYtgniceux33iZZJM9BJL0'

export default {
    name: 'App',
    components: {
        SearchBar,
    },
    methods: {
        onTermChange(searchTerm) {
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm,
                }
            }).then(response => console.log(response))
        }
    }
};

</script>