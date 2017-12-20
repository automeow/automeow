<template>
  <div
    class="meow"
    v-bind:style="{
      top: `${top}%`,
      left: `${left}%`,
      opacity,
      transitionDuration: `${transitionDuration}s`,
      animationDuration: `${animationDuration}s`,
      fontSize: `${fontSize}em`
    }"
    v-on:click="onClick"
  >
    <div
      class="tumble"
      v-bind:style="{
        transform: `rotate3d(${rotateX}, ${rotateY}, ${rotateZ}, ${rotateAngle}deg)`,
        transitionDuration: `${transitionDuration}s`
      }"
    >
      Meow
    </div>
  </div>
</template>

<script>
export default {
  name: 'meow',
  data () {
    return {
      timer: null,
      top: -10,
      left: 0,
      opacity: 1,
      transitionDuration: 15,
      animationDuration: 5,
      fontSize: 1,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0,
      rotateAngle: 180
    }
  },
  mounted () {
    this.timer = setTimeout(this.beginMovement.bind(this), 0)
  },
  methods: {
    onClick () {
      clearTimeout(this.timer)
      this.endMovement()
      this.$emit('click')
    },
    beginMovement () {
      this.top = 101
      this.left = Math.floor(Math.random() * 100)
      this.opacity = 0.1 + (Math.random() * 0.9)
      this.transitionDuration = 5 + Math.ceil(Math.random() * 10)
      this.fontSize = Math.random()
      this.animationDuration = 2 + Math.ceil(Math.random() * 13 * this.fontSize)
      this.rotateX = Math.random()
      this.rotateY = Math.random()
      this.rotateZ = Math.random()
      this.rotateAngle = Math.random() * 360

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

  .tumble {
    transition-timing-function: ease;
    transition-property: transform;
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
