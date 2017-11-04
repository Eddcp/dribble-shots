<template>
  <div class="modal" :class='active'>
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Shot Details</p>
        <button @click="closeModal" class="delete" aria-label="close"></button>
      </header>
      <section class="modal-card-body">
        <slot></slot>
      </section>
      <footer class="modal-card-foot">
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app-modal',
  props: ['active'],
  data() {
    return {

    }
  },
  methods: {
    closeModal() {
      this.$emit('close-modal')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '.././styles/variables.scss';

.modal-container {
  background-color: $color-wild-sand;
}
</style>
