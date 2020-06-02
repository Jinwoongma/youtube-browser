<template>
  <div id="app" class='container'>
    <p class='main-logo'>YouTube Browser</p>
    <search-bar @inputChange="onInputChange"></search-bar> <!-- 3단계 -->
    <div class="row">
      <video-detail :video="selectedVideo"> </video-detail>
      <video-list @videoSelect="onVideoSelect" :videos="videos"></video-list>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from './components/SearchBar' // 1단계
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'app', 
  components: { // 2단계
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return {
      videos: [],
      selectedVideo: null,
    }
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video
    },
    onInputChange(inputValue) {
      console.log(inputValue)
      axios.get(API_URL, {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          maxResults: 10,
          q: inputValue,
        }
      })
      .then(response => {
        response.data.items.forEach(item => {
          const parser = new DOMParser()
          const doc = parser.parseFromString(item.snippet.title, 'text/html')
          item.snippet.title = doc.body.innerText
        }) 
        this.videos = response.data.items
        this.selectedVideo = this.videos[0]
      })
      .catch(error => { 
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin-top: 60px;
    margin-bottom: 60px;
  }
  .main-logo {
    color: red;
    text-align: center;
    font-weight: 600;
    font-size: 50px;
  }
</style>