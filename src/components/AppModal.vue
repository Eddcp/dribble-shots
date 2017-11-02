<template>
  <div class="modal" :class='active'>
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="modal-container box">
          <slot></slot>
      </div>
    </div>
    <button @click="closeModal" class="modal-close is-large" aria-label="close"></button>
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
