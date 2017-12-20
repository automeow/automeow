<template>
  <div id="app">
    <audio
      v-for="sound in sounds"
      :key="sound"
      ref="meows"
      :src="`static/${sound}.mp3`" />

    <div class="counter">
      {{ meowCount }}
    </div>

    <meow
      v-for="m in meowCount"
      :key="m"
      v-on:click="playSound"
    />
  </div>
</template>

<script>
import Meow from './components/meow'

export default {
  name: 'app',
  components: {
    Meow
  },
  data () {
    return {
      meowCount: 0,
      sounds: [
        'meow1',
        'meow2',
        'meow3'
      ]
    }
  },
  mounted () {
    this.increaseMeowCount()
  },
  methods: {
    increaseMeowCount () {
      this.meowCount++

      setTimeout(
        this.increaseMeowCount.bind(this),
        Math.ceil(Math.random() * 2500)
      )
    },
    playSound () {
      const index = Math.floor(this.$refs.meows.length * Math.random())
      this.$refs.meows[index].play()
    }
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

    .counter {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      font-size: 40vw;
      opacity: 0.04;
      pointer-events: none;
    }
  }
}
</style>
