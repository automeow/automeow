<template>
  <div
    class="meow"
    v-bind:style="{
      top: `${top}%`,
      left: `${left}%`,
      opacity,
      transitionDuration: `${transitionDuration}s`
    }"
    v-on:click="onClick"
  >
    Meow
  </div>
</template>

<script>
export default {
  name: 'meow',
  data () {
    return {
      top: -10,
      left: 0,
      opacity: 1,
      transitionDuration: 15,
      timer: null
    }
  },
  mounted () {
    this.timer = setTimeout(this.beginMovement.bind(this), 0)
  },
  methods: {
    onClick () {
      clearTimeout(this.timer)
      this.endMovement()
    },
    beginMovement () {
      this.top = 101
      this.left = Math.floor(Math.random() * 100)
      this.opacity = 0.1 + (Math.random() * 0.9)
      this.transitionDuration = 5 + Math.ceil(Math.random() * 10)

      this.timer = setTimeout(
        this.endMovement.bind(this),
        this.transitionDuration * 1000
      )
    },
    endMovement () {
      this.top = -10
      this.transitionDuration = 0

      this.timer = setTimeout(this.beginMovement.bind(this), 1000)
    }
  }
}
</script>

<style scoped lang="less">
.meow {
  position: absolute;
  animation: drift 5s ease-in-out infinite;
  cursor: pointer;
  transition-timing-function: linear;
  transition-property: top;
}

@keyframes drift {
  0% {
    transform: translateX(-300%);
  }
  50% {
    transform: translateX(300%);
  }
  100% {
    transform: translateX(-300%);
  }
}
</style>
