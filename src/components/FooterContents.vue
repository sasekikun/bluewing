<template>
  <footer :style="styles" class="footer_contents">
    <div>
      <a v-if="logoImage && logoImage.link" :href="logoImage.link">
        <img :src="logoImage.src" :height="logoImage.height" :alt="logoImage.alt">
      </a>

      <img v-else-if="logoImage && logoImage.src" :src="logoImage.src" :height="logoImage.height" :alt="logoImage.alt">

      <slot/>
    </div>

    <p v-if="copyRight" class="copy_right">
      &copy; {{ copyRight }}
    </p>
  </footer>
</template>

<script>
export default {
  name: 'FooterContents',
  props: {
    styleObject: {
      type: Object,
      default: () => ({
        textColor: '#f4f4f4',
        backgroundColor: '#191944'
      })
    },
    logoImage: {
      type: Object,
      default: () => ({
        src: '',
        link: '',
        height: '',
        alt: ''
      })
    },
    copyRight: {
      type: String,
      default: ''
    }
  },
  computed: {
    styles() {
      return {
        ...this.styleObject,
        color: this.styleObject.textColor,
        'background-color': this.styleObject.backgroundColor
      }
    }
  }
}
</script>

<style lang="scss" scoped>
footer div {
  padding: 1em;
}
.copy_right {
  text-align: center;
  border-top: 1px dotted;
  padding: 8px 0;
  margin: 0;
}
</style>
