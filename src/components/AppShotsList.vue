<template>
  <div>
    <ul class="columns is-multiline is-centered">
        <li class="shot-item column"
            v-if="shots && shots.length"
            v-for="shot in filteredShotsList"
            @click="onShotClick(shot)"
            :class="imageType === 'small' ?
              'is-full-mobile is-half-mobile is-one-quarter-tablet':
              'is-half-tablet'">
          <app-shot :shot="shot"></app-shot>
        </li>
        <li v-for="error in errors">
            {{error.message}}
        </li>
    </ul>
    <infinite-loading @infinite="infiniteHandler" spinner="bubbles"></infinite-loading>
  </div>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import AppShot from './AppShot.vue';
import InfiniteLoading from 'vue-infinite-loading';
import { EventBus } from '.././main.js';


const ACCESS_TOKEN = '49b5dd154d7308e1602a9a973e58fcce107fa2d3e1a8741643915aa8beaaf7e6'
const API_URL =  'https://api.dribbble.com/v1/shots/'

export default {
  name: 'app-shots-list',
  data() {
    return {
      shots: [],
      errors: [],
      search: '',
      currentPage: 1,
      imageType: 'small'
    }
  },
  methods: {
    addImageSizeProperty() {
      if(this.imageType === 'small'){
        this.shots.forEach((shot, index) => {
            Vue.set(shot, 'imageSize', shot.images.teaser)
        })
      } else {
        this.shots.forEach((shot, index) => {
            Vue.set(shot, 'imageSize', shot.images.normal)
        })
      }
    },
    updateCurrentPage() {
      this.currentPage += 1
    },
    infiniteHandler($state) {
      axios.get(API_URL, {
        params: {
          page:this.currentPage,
          access_token:ACCESS_TOKEN
        }
      }).then(response => {
        if (response.data) {
          this.shots = this.shots.concat(response.data);
          this.addImageSizeProperty()
          this.updateCurrentPage()
          $state.loaded()
        }
        else {
          $state.complete()
        }
      }).catch(e => {
        this.errors.push(e)
      })
    },
    onShotClick(shot) {
      EventBus.$emit('open-modal', shot)
    },
    updateSearch(search) {
      this.search = search
    },
    resizeImage(size) {
      if(size === 'normal') {
          this.imageType = 'normal'
          this.shots.forEach((shot, index) => {
              Vue.set(shot, 'imageSize', shot.images.normal)
          })
      } else {
        this.imageType = 'small'
        this.shots.forEach((shot, index) => {
            Vue.set(shot, 'imageSize', shot.images.teaser)
        })
      }
    }
  },
  mounted() {
    EventBus.$on('filter-shots-by-name', this.updateSearch )
    EventBus.$on('resize-image', this.resizeImage)
  },
  computed: {
    filteredShotsList() {
      return this.shots.filter(shot => {
        return shot.user.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  components: {
    AppShot,
    InfiniteLoading
  }
}
</script>

<style lang="scss" scoped>

ul {
  text-align: center;
}

li {
  display: inline-block;
}

@media screen and (max-width: 500px) {
  .is-full-mobile {
    flex: none;
    width: 100%;
  }
}
</style>
