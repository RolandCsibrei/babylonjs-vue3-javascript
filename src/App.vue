<template>
  <babylons-js-scene />
</template>

<script>
import BabylonsJsScene from './components/BabylonJsScene.vue'

export default {
  name: 'App',
  components: {
    BabylonsJsScene
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
