<template>
    <div>

        <n-card title="Now Playing" size="small">
            <div class="d-flex align-items-center" v-if="isPlaying == 'true'">
                <img class="rotating" :src="trackImg" :alt="trackName">
                <div class="ms-3">
                    <p><b>{{ trackName }}</b> from <b>{{ trackAlbum }}</b></p>
                    <p>By <b>{{ trackArtist }}</b></p>
                </div>
            </div>
            <div v-else>
                <p>NOT PLAYING ANY TRACKS!</p>
            </div>
        </n-card>

    </div>
</template>

<script>
import { NCard, NRate } from 'naive-ui';

export default {
    name: "NowPlayingCard",
    components: {
        NCard,
        NRate
    },
    props: {
        isPlaying: Boolean,
        trackName: String,
        trackAlbum: String,
        trackImg: String,
        trackArtist: String
    }
};
</script>

<style scoped>
p {
    line-height: 20px;
    padding: 0;
    margin: 0;
}

img {
    height: 40px;
    width: 40px;
    object-fit: cover;
    border-radius: 50%;
}

@keyframes rotating {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.rotating {
    animation: rotating 20s linear infinite;
}
</style>