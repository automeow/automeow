<template>
  <div id="app">
    <meow />
  </div>
</template>

<script>
import Meow from './components/meow'

export default {
  name: 'app',
  components: {
    Meow
  }
}
</script>

<style lang="less">
body {
  margin: 0;
  padding: 0;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  overflow: hidden;

  #app {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
}
</style>
