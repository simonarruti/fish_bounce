<template>
  <div id="app">
    <wrapper></wrapper>
  </div>
</template>

<script>
  import Wrapper from '@/components/Wrapper'

  export default {
    name: 'app',
    components: {
      Wrapper
    }
  }
</script>

<style>
  body {
    margin: 0;
    padding: 0;
  }
  #app {
    overflow: hidden;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
</style>
