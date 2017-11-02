<template>
    <header id="header" class="header">
      <div class="search-input">
        <input class="input" type="text" placeholder="Search" v-model="search" @input="onChange"/>
      </div>
    </header>
</template>

<script>
import { EventBus } from '.././main.js';

export default {
  name: 'app-header',
  data() {
    return {
      search: ''
    }
  },
  methods: {
    onChange() {
      EventBus.$emit('filter-shots-by-name', this.search)
    }
  }
}
</script>

<style lang="scss">
@import '.././styles/variables.scss';

.header {
  background: $color-grey-darker;
  height: 56px;
}

.search-input {
  position: absolute;
  top: 10px;
  right: 30px;
}

</style>
