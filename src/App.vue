<template>
  <div id="app">
    <Randomizer/>
  </div>
</template>

<script>
import Randomizer from './components/Randomizer'

export default {
  name: 'App',
  components: {
    Randomizer
  }
}
</script>

<style lang="scss">
@import "src/scss/variables";
@import url('https://fonts.googleapis.com/css?family=VT323');

html {
  background-color: $primary-color;
}
#app {
  font-family: VT323, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $secondary-color;
  display: flex;
  justify-content: center;
}
</style>
