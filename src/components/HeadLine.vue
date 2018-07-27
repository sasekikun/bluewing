<template>
  <h2 :style="styles">
    <slot>
      Headline Sample Text
    </slot>
  </h2>
</template>

<script>
export default {
  name: 'HeadLine',
  props: {
    textColor: {
      type: String,
      default: '#191944'
    },
    fontWeight: {
      type: String,
      default: ''
    },
    fontSize: {
      type: String,
      default: '32px'
    },
    textAlign: {
      type: String,
      default: 'left'
    }
  },
  computed: {
    styles() {
      return {
        color: this.textColor,
        fontWeight: this.fontWeight,
        fontSize: this.fontSize,
        textAlign: this.textAlign
      }
    }
  }
}
</script>

<style scoped>
</style>
