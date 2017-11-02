<template>
  <div id="app">
    <app-header></app-header>
    <app-content></app-content>
    <app-footer></app-footer>
  </div>
</template>

<script>

import AppHeader from './components/AppHeader.vue';
import AppContent from './components/AppContent.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'app',
  data() {
    return {
      
    }
  },
  components: {
    AppHeader,
    AppContent,
    AppFooter
  }

}
</script>

<style lang="scss">
@import './styles/main.scss';
</style>
