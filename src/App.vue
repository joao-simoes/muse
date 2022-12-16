<template>
  <n-config-provider :theme="darkTheme">
    <n-loading-bar-provider>
      <div class="container-fluid">
        <router-view></router-view>
      </div>
    </n-loading-bar-provider>
  </n-config-provider>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700&display=swap');

#app {
  background-color: #202020;
  max-width: 100vw;
  min-height: 100vh;
  overflow-x: hidden;
  color: white;
}

* {
  font-family: 'Poppins', sans-serif;
  color: #DDDDDD;
}
</style>

<script>
import { NLoadingBarProvider, NConfigProvider, darkTheme } from 'naive-ui'

export default ({
  components: {
    NLoadingBarProvider,
    NConfigProvider
  },
  setup() {
    return {
      darkTheme
    }
  }
})
</script>