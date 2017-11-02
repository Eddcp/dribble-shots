<template lang="html">
  <div v-if="shot">
    <div class="shot-detailed__header tile is-parent">
      <img class="shot-detailed__avatar" :src="shot.user.avatar_url" />
      <div class="shot-detailed__title">
        <h1 class="shot-detailed__title--image">{{shot.title}}</h1>
        <h2 class="shot-detailed__title--information">
          by <a href="#">{{shot.user.name}}</a>
          <span v-if="shot.team">for <a href="#">{{shot.team.name}}</a></span>
        </h2>
      </div>
    </div>
    <div class="shot-detailed__container tile">
      <div class="tile">
        <div class="tile is-parent is-8">
          <div class="tile is-child">
            <img :src="shot.images.normal" />
            <div v-html="shot.description"></div>
          </div>
        </div>
        <div class="tile is-parent">
          <span>Like?</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['shot'],
  data() {
    return {
    }
  },
  methods: {

  },
  created() {
  }
}
</script>

<style lang="scss" scoped>
.shot-detailed {
   &__avatar {
       width: 48px;
       height: 48px;
       border-radius: 50%;
   }

   &__title {

   }
}
</style>
