<template lang="html">
  <div v-if="shot" class="shot-container">
    <img :src="shot.imageSize"/>
    <div>
      <img class="shot-container__avatar" :src="shot.user.avatar_url" />
      <span>{{shot.user.name}}</span>
    </div>
  </div>
</template>

<script>
import { EventBus } from '.././main.js';

export default {
  props:['shot'],
  data() {
    return {
    }
  },
  methods: {
    resizeImage(size) {
      if(size === 'normal') {
          this.shot.imageSize = this.shot.images.normal
      } else {
          this.shot.imageSize = this.shot.images.teaser
      }
    }
  },
  created() {
    EventBus.$on('resize-image', this.resizeImage)
  }
}
</script>

<style lang="scss" scoped>

.shot-container {
  display: block;
  padding: 10px;
  background: #fff;
  margin: 10px;
  cursor: pointer;

  &__avatar {
    width: 16px;
    height: 16px;
    margin: 1px 5px 0 0;
    border-radius: 50%;
  }
}

</style>
