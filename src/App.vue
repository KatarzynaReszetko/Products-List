<template>
  <AppContainer />
</template>

<script>
import AppContainer from './components/AppContainer.vue'

export default {
  name: 'App',
  components: { AppContainer },
}
</script>

<style>
#app {
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 30px;
}
</style>
