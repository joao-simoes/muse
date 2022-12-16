<template>
  <div>
    <img class="logo ms-5 mt-4" :src="require('../assets/' + imgSrc + '.png')">
  </div>
</template>

<script>
export default {
  name: 'TopHeader',
  props: {
    imgSrc: String
  }
}
</script>

<style scoped>
.logo {
  height: 60px;
}
</style>