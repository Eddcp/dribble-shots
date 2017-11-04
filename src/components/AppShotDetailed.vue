<template lang="html">
  <div v-if="shot">
    <div class="shot-detailed__header tile is-parent">
      <img class="shot-detailed__avatar" :src="shot.user.avatar_url" />
      <div class="shot-detailed__title">
        <h1 class="shot-detailed__title--image">{{shot.title}}</h1>
        <h2>
          by <a href="#">{{shot.user.name}}</a>
          <span v-if="shot.team">for <a href="#">{{shot.team.name}}</a></span>
        </h2>
      </div>
    </div>
    <div class="shot-detailed__container columns">
        <div class="column is-8">
          <div class="">
            <img v-if="shot.images.hidpi" :src="shot.images.hidpi" />
            <img v-else :src="shot.images.normal" />
            <div v-html="shot.description" class="shot-detailed__description"></div>
          </div>
        </div>
        <div class="column is-4">
            <span :class="[{'shot-detailed__like--liked' : shot.isLiked},
                          'shot-detailed__like']"
                  @click="toggleLike(shot)"
                  >
            </span>
            <span>Like?</span>
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
    toggleLike(shot) {
      shot.isLiked = !shot.isLiked
    }
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
      padding-left: 20px;

      &--image {
        font-size: 20px;
        font-weight: 700;
      }
   }

   &__description {
     & p {
       text-align: justify;
       margin: 0 10px;
     }
   }

   &__like {
     display:inline-block;
     width: 20px;
     height: 20px;
     opacity: 0.3;
     background-size: 20px 20px;
     background-image: url('../assets/images/icon-like.png');
     background-repeat: no-repeat;
     cursor:pointer;

     &--liked {
       opacity: 1;
     }
   }
}
</style>
