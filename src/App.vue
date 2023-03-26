<template>
  <generator />
</template>

<script>
import generator from './components/generator.vue'

export default {
  name: 'App',
  components: {
    generator
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

@media only screen and (max-width: 565px) {
  #app {
    width: 90%;
  }

  .containerDiv {
    width: 100%;
  }

  button {
    text-align: center;
  }
}
</style>
