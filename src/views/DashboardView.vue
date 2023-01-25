<template>
  <div class="bg"></div>
  <NowPlayingCard class="NowPlayingCard" :isPlaying="isPlaying" :trackName="trackName" :trackAlbum="trackAlbum"
    :trackImg="trackImg" :trackArtist="trackArtist" />
  <div class="header">
    <UserHeader imgSrc="logo_text" :imgAvatar="imgAvatar" :username="username" :email="email" :followers="followers" />
  </div>
  <div class="container position-relative">
    <div class="dashboard text-center">
      <h2>I'm curious about my top <input class="text-center" placeholder="10" type="text" name="amount" id="amount"
          size="2" maxlength="2">
        most listened
        <select id="type">
          <option value="artists">artists</option>
          <option value="tracks">tracks</option>
        </select> !
      </h2>
      <n-button secondary round size="large" class="mt-3" v-on:click="fetchUserTop">
        Search
      </n-button>
    </div>
    <div v-if="top.length > 0" class="mt-5">

      <n-divider title-placement="left">
        <h3>Top {{ top.length }}</h3>
      </n-divider>
      <div class="row">

        <ArtistCard v-if="type == 'artists'" v-for="artist in top" class="col-12 col-md-6 col-lg-4 my-2"
          :name="artist.name" :genres="artist.genres" :popularity="artist.popularity" :rank="top.indexOf(artist) + 1"
          :imgSrc="artist.images[0].url" :followers="artist.followers.total" />

        <TrackCard v-if="type == 'tracks'" v-for="track in top" class="col-12 col-md-6 col-lg-4 my-2" :name="track.name"
          :releaseDate="track.album.release_date" :artist="track.artists[0].name" :album="track.album.name"
          :rank="top.indexOf(artist) + 1" :imgSrc="track.album.images[0].url" />

      </div>
    </div>
  </div>
</template>






<script>
import UserHeader from '../components/UserHeader.vue'
import ArtistCard from '../components/ArtistCard.vue'
import TrackCard from '../components/TrackCard.vue'
import NowPlayingCard from '../components/NowPlayingCard.vue'
import { NButton, NDivider } from 'naive-ui'

export default {
  name: 'DashboardView',
  data() {
    return {
      imgAvatar: null,
      username: null,
      email: null,
      followers: null,
      top: [],
      isPlaying: "false",
      trackName: null,
      trackAlbum: null,
      trackImg: null,
      trackArtist: null,
      type: null
    }
  },
  components: {
    UserHeader,
    ArtistCard,
    TrackCard,
    NowPlayingCard,
    NButton,
    NDivider
  },
  methods: {
    fetchUserTop() {
      let amount = document.getElementById('amount').value
      this.type = document.getElementById('type').value

      fetch(`https://api.spotify.com/v1/me/top/${this.type}?limit=${amount}`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer ' + localStorage.getItem('access_token')
        }
      }).then((async response => {
        let data = await response.json()
        this.top = data.items
      }))
    },
    fetchUserPlayback() {
      fetch(`https://api.spotify.com/v1/me/player/currently-playing`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer ' + localStorage.getItem('access_token')
        }
      }).then((async response => {
        let data;

        try {
          data = await response.json()

          this.isPlaying = "true"
          this.trackArtist = data.item.album.artists[0].name
          this.trackAlbum = data.item.album.name
          this.trackName = data.item.name
          this.trackImg = data.item.album.images[0].url
        } catch (err) {
          console.log(err)
          this.isPlaying = "false"
        }

        setTimeout(this.fetchUserPlayback(), 500000)

      }))
    }
  },
  beforeMount() {

    localStorage.setItem('access_token', this.$route.query.access_token)

    this.fetchUserPlayback()

    fetch('https://api.spotify.com/v1/me', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + localStorage.getItem('access_token')
      }
    }).then((async response => {
      let data = await response.json()
      this.imgAvatar = data.images[0].url
      this.email = data.email
      this.username = data.display_name
      this.followers = data.followers.total + ' followers'
    }))

  }
}
</script>






<style scoped>
.bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-image: url('../assets/background.jpeg');
  background-size: cover;
  filter: grayscale('100%');
  opacity: 2%;
}

.header {
  background-color: #202020;
}

h1 {
  font-weight: 500;
  font-size: 100px;
}

.dashboard {
  margin-top: 15%;
}

input,
select {
  background-color: rgba(255, 255, 255, 0);
  border: none;
  border-bottom: 1px dashed white;
}

.NowPlayingCard {
  width: 30%;
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 100;
  opacity: 40%;
  transition: 0.2s ease-in-out;
}

.NowPlayingCard:hover {
  opacity: 100%;
  transition: 0.s ease-in-out;
}


@media only screen and (max-width: 768px) {
  .NowPlayingCard {
    width: 90%;
    position: fixed;
    bottom: 20px;
    right: 5%;
    z-index: 100;
    opacity: 40%;
    transition: 0.2s ease-in-out;
  }
}
</style>