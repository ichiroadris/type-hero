<template>
  <div id="app" class="h-screen bg-gray-300">
    <navbar></navbar>
    <typearea></typearea>
  </div>
</template>

<script>
import navbar from './components/navbar.vue'
import typearea from './components/typearea'

export default {
  name: 'App',
  components: {
    navbar,
    typearea
  }
}
</script>

<style lang="scss">
</style>
