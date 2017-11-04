<template lang="html">
  <div v-if="shot" class="shot-container">
    <img :src="shot.imageSize"/>
    <div>
      <img class="shot-container__avatar" :src="shot.user.avatar_url" />
      <span class="shot-container__name">{{shot.user.name}}</span>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import { EventBus } from '.././main.js';

export default {
  props:['shot'],
  data() {
    return {
    }
  },
  methods: {

  },
  created() {
    Vue.set(this.shot, 'isLiked', false)
  }
}
</script>

<style lang="scss" scoped>

.shot-container {
  display: inline-block;
  padding: 10px;
  background: #fff;
  margin: 10px;
  cursor: pointer;
  box-sizing:border-box;
  min-width:200px;
  min-height:150px;

  &__avatar {
    width: 16px;
    height: 16px;
    margin: 1px 5px 0 0;
    border-radius: 50%;
  }

  &__name {
    font-size: 14px;
  }
}

</style>
