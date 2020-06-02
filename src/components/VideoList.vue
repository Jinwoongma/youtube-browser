<template>
    <div class='list-container col-lg-4'>
        <h5>검색 결과</h5>
        <ul class='list-group '>
            <video-list-item 
                v-for="video in videos" 
                :key="video.etag" 
                :video="video"
                @videoSelect="onVideoSelect"> 
            </video-list-item>
        </ul>
    </div>
    
</template>

<script>
import VideoListItem from './VideoListItem'

export default {
    name: 'VideoList',
    components: {
        VideoListItem,
    },
    methods: {
        onVideoSelect(video) {
            this.$emit('videoSelect', video)
        }
    },
    props: {
        videos: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style>
    .list-group{
        max-height: 500px;
        margin-bottom: 10px;
        overflow:scroll;
        -webkit-overflow-scrolling: touch;
    }
</style>