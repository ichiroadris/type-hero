<template>
  <div id="app" class="h-screen bg-teal-600 font-mono flex flex-col justify-between">
    <navbar></navbar>
    <typearea v-bind:randomWords="randomWords"></typearea>
    <footerapp></footerapp>
  </div>
</template>

<script>
import navbar from './components/navbar.vue'
import typearea from './components/typearea.vue'
import footerapp from './components/footerapp.vue'
import json from './assets/texts.json'


export default {
  name: 'App',
  components: {
    navbar,
    typearea,
    footerapp
  },
  data() {
      return {
          randomWords: json
      }
  }
}
</script>

<style lang="scss">
</style>
