<template>
  <TopHeader imgSrc="logo_round" class="position-fixed top-0 start-0 vw-100" />
  <div id="parallax"></div>
  <div class="position-fixed w-100 text-center top-50 translate-middle-y">
    <h1>MUSE.</h1>
    <h3>WHAT AM I UP TO?</h3>
    <a href="http://127.0.0.1:3100/login" class="m-auto">
      <img class="bttLogin mt-3" :src="require('../assets/btt_spotify.png')" alt="Login with Spotify">
    </a>
  </div>
</template>

<script>
import TopHeader from '../components/TopHeader.vue'

export default {
  name: 'HomeView',
  components: {
    TopHeader
  },
  mounted() {
    (function () {
      // Add event listener
      document.addEventListener("mousemove", parallax);
      const elem = document.querySelector("#parallax");
      // Magic happens here
      function parallax(e) {
        let _w = window.innerWidth / 2;
        let _h = window.innerHeight / 2;
        let _mouseX = e.clientX;
        let _mouseY = e.clientY;
        let _depth1 = `${20 - (_mouseX - _w) * 0.01}% ${20 - (_mouseY - _h) * 0.01}%`;
        let _depth2 = `${20 - (_mouseX - _w) * 0.01}% ${20 - (_mouseY - _h) * 0.01}%`;
        let _depth3 = `${20 - (_mouseX - _w) * 0.05}% ${20 - (_mouseY - _h) * 0.01}%`;
        let x = `${_depth1}, ${_depth2}, ${_depth3}`;

        elem.style.backgroundPosition = x;
      }

    })();
  },
}
</script>

<style scoped>
#parallax {
  position: fixed;
  width: 100vw;
  height: 100vh;
  background-image: url("../assets/background.jpeg");
  background-repeat: no-repeat;
  background-position: center;
  background-position: 50% 50%;
  background-size: cover;
  filter: grayscale(100%);
  opacity: 4%;
}

h1 {
  font-size: 100px;
  font-weight: 600;
}

h3 {
  font-weight: 100;
}

.bttLogin {
  width: 20%;
}
</style>