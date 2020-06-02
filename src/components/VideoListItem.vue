<template>
    <li  @click="onVideoSelect" class='list-group-item'>
        <img :src="thumbnailUrl">
        <div class='media-container'>
            <div class='media-body '>
                <p v-html="video.snippet.title"></p>
            </div>
            <div class='midea-subbody'>
                <small>{{ video.snippet.channelTitle }}</small>
            </div>
        </div>
        
    </li>
</template>

<script>

export default {
    name: 'VideoListItem',
    props: {
        video: {
            type: Object,
            required: true,
        }
    },
    methods: {
        onVideoSelect() {
            this.$emit('videoSelect', this.video)
        }
    },
    computed: {
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url
        }
    }
}
</script>

<style scoped>
    img {
        margin-right: 20px;
    }
    li {
        display: flex;
        cursor: pointer;
    }
    li:hover {
        background-color: #eee;
    }
    .media-body {
        margin: 0 auto;
        display:-webkit-box;
        -webkit-line-clamp:2;
        -webkit-box-orient:vertical;
        height:40px;
        line-height:20px;
        overflow:hidden;
        text-overflow:ellipsis;
        font-weight: bold;
     }
</style>