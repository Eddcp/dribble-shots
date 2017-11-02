<template>
  <ul class="flex-container">
      <li v-if="shots && shots.length"
          v-for="shot in filteredShotsList"
          @click="onShotClick(shot)">
        <app-shot :shot="shot"></app-shot>
      </li>
      <li v-for="error in errors">
          {{error.message}}
      </li>
  </ul>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import { EventBus } from '.././main.js';
import AppShot from './AppShot.vue';

const ACCESS_TOKEN = '7be90c891d972d92b9451c465e51d0796932a45a5f11f60d18423983480abacb'
const API_URL =  'https://api.dribbble.com/v1/shots/'

export default {
  name: 'app-shots-list',
  data() {
    return {
      shots: [],
      errors: [],
      search: ''
    }
  },
  methods: {
    addImageSizeProperty() {
      this.shots.forEach((shot, index) => {
          Vue.set(shot, 'imageSize', shot.images.teaser)
      })
    },
    getShots(){
      axios.get(`${API_URL}?access_token=${ACCESS_TOKEN}`)
        .then(response => {
          this.shots = response.data
          this.addImageSizeProperty()
        })
        .catch(e => {
          this.errors.push(e)
        })
    },
    onShotClick(shot) {
      EventBus.$emit('open-modal', shot)
    },
    updateSearch(search) {
      this.search = search
    }
  },
  created() {
    this.getShots()
  },
  mounted() {
    EventBus.$on('filter-shots-by-name', this.updateSearch )
  },
  computed: {
    filteredShotsList() {
      return this.shots.filter(shot => {
        return shot.user.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  components: {
    AppShot
  }
}
</script>

<style lang="scss" scoped>

</style>
