<template>
  <div
    id="app"
    v-bind:style="{ backgroundImage }"
    v-on:click="updateBackgroundImage"
  >
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

const CAT_API_BASE = 'http://thecatapi.com/api/images/get'

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
      ],
      backgroundImages: [CAT_API_BASE]
    }
  },
  computed: {
    backgroundImage () {
      return this.backgroundImages.map(i => `url(${i})`).join(', ')
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
      this.meowCount--
    },
    updateBackgroundImage () {
      this.backgroundImages
        .unshift(`${CAT_API_BASE}?date=${new Date().getTime()}`)

      setTimeout(this.removeUnusedBackgroundImages.bind(this), 5000)
    },
    removeUnusedBackgroundImages () {
      this.backgroundImages = [this.backgroundImages[0]]
    }
  }
}
</script>

<style lang="less">
body {
  margin: 0;
  padding: 0;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-shadow: 0 0 0.3em #2c3e50;
  color: #fff;
  overflow: hidden;

  #app {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    background-size: cover;

    .counter {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      font-size: 40vw;
      opacity: 0.2;
      pointer-events: none;
    }
  }
}
</style>
