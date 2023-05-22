<template>
  <ChessContainer />
</template>

<script>
import ChessContainer from './containers/ChessContainer.vue'

export default {
  name: 'App',
  components: {
    ChessContainer
  }
}
</script>

<style>
:root {
  /* Colors */
  --main-dark-1: #000000;
  --main-dark-2: #41403e;
  --main-dark-3: #383734;
  --main-dark-4: #51504c;
  --main-dark-5: #41403e;
  --main-dark-6: hsla(0,0%,100%,.2);

  --main-light-1: #ffffff;
  --main-light-2: #d0cfcf;
  --main-light-3: #c9c9c8;

  --dark-cell: #b58962;
  --light-cell: #f0dab5;
  --active-cell: #ffff00;
  --hint-cell: #de9280;

  /* Opacities */
  --light-opacity: 80%;

  /* Font Weights */
  --font-bold: 700;

  /* Font Sizes */
  --font-size-md: 14px;

  /* Media Sizes */
  --media-md: 920px;

  /* Spacing Sizes */
  --space-xsm: 2px;
  --space-sm: 4px;
  --space-md: 8px;
  --space-lg: 16px;
  --space-xl: 32px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0;
}
html {
    background: #51504c;

}
</style>
