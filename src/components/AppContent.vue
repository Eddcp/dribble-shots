<template>
  <main id="main-content">
    <div class="resize-bar">
        <div class="resize-buttons">
          <button @click="changeImageSize('small')">pequeno</button>
          <button @click="changeImageSize('normal')">maior</button>
        </div>
    </div>
    <div class="wrapper">
      <section>
          <app-shots-list></app-shots-list>
      </section>
      <app-modal :active="activateModal" @close-modal="close">
          <app-shot-detailed v-if="shot" :shot="shot"></app-shot-detailed>
      </app-modal>
    </div>
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
    },
    close() {
      this.activateModal = ''
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
  padding: 40px;
}

.resize-bar {
  width: 100%;
  min-height: 50px;
  border-bottom: 1px solid $color-mercury;
  background: $color-white;
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
