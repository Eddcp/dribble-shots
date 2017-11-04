<template>
    <header id="header" class="header">
      <div class="dribble-logo">
      </div>
      <div class="search-input">
        <span></span>
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
  padding-left: 20px;
}

.search-input {
  position: absolute;
  top: 10px;
  right: 30px;

}

.dribble-logo {
  width: 76px;
  height: 56px;
  background-repeat: no-repeat;
  background-position: 0 50%;
  background-image: url('../assets/images/logo.png');

  @media screen and (max-width: 400px) {
    display: none;
  }
}

</style>
