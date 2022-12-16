<template>
  <div class="d-flex justify-content-between mt-4 align-items-center">
    <div>
      <img class="logo ms-5" :src="require('../assets/' + imgSrc + '.png')">
    </div>
    <div styles="width: 25%;" class="d-flex align-items-center me-5">
      <div class="text-end me-2">
        <h5>{{ username }}</h5>
        <h6>{{ email }}</h6>
      </div>
      <n-badge :value="followers">
        <n-avatar round :size="64" :src="imgAvatar" object-fit="cover" />
      </n-badge>
    </div>
  </div>
</template>

<script>
import { NAvatar, NBadge } from 'naive-ui';

export default {
  name: 'UserHeader',
  components: {
    NAvatar,
    NBadge
  },
  props: {
    imgSrc: String,
    imgAvatar: String,
    username: String,
    email: String,
    followers: String
  }
}
</script>

<style scoped>
.logo {
  height: 60px;
}

h5 {
  font-weight: 400;
}

h6 {
  font-weight: 200;
}
</style>