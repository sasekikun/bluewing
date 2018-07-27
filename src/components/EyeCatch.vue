<template>
  <div id="EyeCatch" ref="eye_catch" :style="styleObject"/>
</template>

<script>
export default {
  props: {
    src: {
      type: String,
      default: null
    },
    height: {
      type: Number,
      default: 600
    },
    speed: {
      type: Number,
      default: 0.5
    }
  },
  data: function() {
    return {
      scrollY: 0,
      topPosion: 0
    }
  },
  computed: {
    styleObject() {
      return {
        backgroundPositionY: this.calcParallax(this.scrollY) + 'px',
        backgroundImage: `url(${this.src})`,
        height: this.height + 'px'
      }
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll),
      (this.topPosion = this.$refs.eye_catch.offsetTop)
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.scrollY = window.scrollY
    },
    calcParallax(scrollposition) {
      return -Math.floor(scrollposition - this.topPosion) * this.speed
    }
  }
}
</script>

<style lang="scss" scoped>
#EyeCatch {
  background-repeat: no-repeat;
  background-size: cover;
  background-attachment: fixed;
}
</style>
