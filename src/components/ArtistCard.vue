<template>
    <div>

        <n-card :title="name" size="small">
            <div class="d-flex justify-content-between">
                <div>
                    <img :src="imgSrc" :alt="name">
                </div>
                <div>
                    <h5 v-if="rank == 1" style="color: gold;">1st Place</h5>
                    <h5 v-if="rank == 2" style="color: silver;">2nd Place</h5>
                    <h5 v-if="rank == 3" style="color: brown;">3rd Place</h5>
                    <br>
                    <p>{{ genres[0] }}</p>
                    <p>{{ followers }} followers</p>
                    <!--<n-rate :id="name" />-->
                </div>
            </div>
        </n-card>

    </div>
</template>

<script>
import { NCard, NRate } from 'naive-ui';

export default {
    name: "ArtistCard",
    components: {
        NCard,
        NRate
    },
    props: {
        name: String,
        rank: Number,
        imgSrc: String,
        popularity: Number,
        url: String,
        genres: Array,
        followers: Number
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