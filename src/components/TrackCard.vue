<template>
    <div>

        <n-card :title="name" size="small">
            <div class="row">
                <div class="col-12 col-md-4">
                    <img :src="imgSrc" :alt="name">
                </div>
                <div class="col-12 col-md-8 mt-2">
                    <p>{{ artist }}</p>
                    <p>{{ album }}</p>
                    <p class="mt-4"> Release Date: {{ releaseDate }}</p>
                </div>
            </div>
        </n-card>

    </div>
</template>

<script>
import { NCard } from 'naive-ui';

export default {
    name: "TrackCard",
    components: {
        NCard
    },
    props: {
        name: String,
        rank: Number,
        artist: String,
        imgSrc: String,
        url: String,
        releaseDate: String,
        album: String
    }
};
</script>

<style scoped>
p {
    line-height: 5px;
}

img {
    height: 80px;
    width: auto;
}
</style>