<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <VideoList :videos="videos"></VideoList>
    </div>
</template>

<script>
    import axios from 'axios';
    import SearchBar from './components/SearchBar'
    import VideoList from './components/VideoList'
    const API_KEY = 'AIzaSyArAI6UVEO771TnrJbVGzD5k0xCY2UlaOc';

    export default {
        name: 'App',
        components: {VideoList, SearchBar},
        data() {
          return {
              videos: []
          }
        },
        methods: {
            onTermChange(searchTerm) {
                axios.get('https://www.googleapis.com/youtube/v3/search', {
                    params: {
                        key: API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: searchTerm
                    }
                }).then(response => {
                    this.videos = response.data.items;
                })
            }
        }
    };
</script>