<template>
  <div
    v-bind:class="{
      meow: true,
      transition
    }"
    ref="element"
    v-bind:style="{
      top: `${top}%`,
      left: `${left}%`
    }">
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
      transition: true
    }
  },
  mounted () {
    setTimeout(this.beginMovement.bind(this), 0)
  },
  methods: {
    beginMovement () {
      this.top = 101
      this.left = Math.floor(Math.random() * 100)
      this.transition = true

      setTimeout(this.endMovement.bind(this), 15000)
    },
    endMovement () {
      this.transition = false
      this.top = -10

      setTimeout(this.beginMovement.bind(this), 1000)
    }
  }
}
</script>

<style scoped lang="less">
.meow {
  position: absolute;
  animation: drift 5s ease-in-out infinite;

  &.transition {
    transition: top 15s linear;
  }
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
