<template>
  <div
    class="meow"
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
      left: Math.floor(Math.random() * 100)
    }
  },
  mounted () {
    setTimeout(this.beginMovement.bind(this), 0)
  },
  methods: {
    beginMovement () {
      this.top = 100

      setTimeout(this.endMovement.bind(this), 16000)
    },
    endMovement () {
      this.$emit('ended')
    }
  }
}
</script>

<style scoped lang="less">
.meow {
  position: absolute;
  transition: top 15s linear;
  animation: drift 5s ease-in-out infinite;
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
