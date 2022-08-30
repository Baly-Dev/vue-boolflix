<template>
  <div id="app">
    <TheHeader />
    <TheMain />
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import TheMain from './components/TheMain.vue'
export default {
  name: 'App',
  components: {
    TheMain,
    TheHeader
  }
}
</script>

<style lang="scss">
@import './assets/scss/global.scss';
</style>
