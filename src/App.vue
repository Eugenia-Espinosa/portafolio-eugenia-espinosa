<template>
  <Portfolio />
</template>

<script>
import Portfolio from './components/PortaFolio.vue'

export default {
  name: 'App',
  components: {
    Portfolio
  }
}
</script>

<style>
html {
  scroll-behavior: smooth;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
}

#app {
  min-height: 100vh;
}
</style>
