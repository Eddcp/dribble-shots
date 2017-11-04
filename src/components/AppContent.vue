<template>
  <main id="main-content">
    <div class="resize-bar">
        <div class="resize-buttons">
          <button class="button is-light small-shots" @click="changeImageSize('small')">
          </button>
          <button class="button is-light large-shots" @click="changeImageSize('normal')"></button>
        </div>
    </div>
    <section class="section">
      <div class="container wrapper">
        <app-shots-list></app-shots-list>
        <app-modal :active="activateModal" @close-modal="close">
            <app-shot-detailed v-if="shot" :shot="shot"></app-shot-detailed>
        </app-modal>
      </div>
    </section>

  </main>
</template>

<script>
import AppShotDetailed from './AppShotDetailed.vue'
import AppShotsList from './AppShotsList.vue'
import AppModal from './AppModal.vue';
import { EventBus } from '.././main.js';

export default {
  name: 'app-content',
  data() {
    return {
      activateModal: '',
      shot: ''
    }
  },
  methods: {
    openModal(shot) {
      this.shot = shot
      this.activateModal = 'is-active'
      document.documentElement.classList.add("is-clipped")
    },
    close() {
      this.activateModal = ''
      document.documentElement.classList.remove("is-clipped");
    },
    changeImageSize(size) {
      EventBus.$emit('resize-image', size)
    }
  },
  created() {
    EventBus.$on('open-modal', this.openModal)
  },
  components: {
    AppShotDetailed,
    AppShotsList,
    AppModal
  }
}
</script>

<style lang="scss" scoped>
@import '.././styles/variables.scss';

.wrapper {
  width: 80%;
}

@media screen and (max-width: 500px) {
  .resize-buttons {
    display: none;
  }

}

.resize-bar {
  width: 100%;
  min-height: 50px;
  border-bottom: 1px solid $color-mercury;
  background: $color-white;
  margin-bottom: 20px;
}

.small-shots {
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-image: url('../assets/images/small.png');
  background-size: 30px 30px;
}

.large-shots {
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-image: url('../assets/images/large.png');
  background-size: 30px 30px;
}

.resize-buttons {
  position: absolute;
  top: 60px;
  right: 30px;

  & button {
    width: 40px;
    height: 40px;
  }
}

</style>
