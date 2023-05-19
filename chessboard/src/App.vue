<template>
  <ChessContainer />
</template>

<script>
import ChessContainer from './components/ChessContainer.vue'

export default {
  name: 'App',
  components: {
    ChessContainer
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
  padding: 20px 0;
}
html {
    background: #51504c;
}
</style>
