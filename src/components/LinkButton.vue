<template>
  <a :href="to" :style="styles" class="link_button" @mouseenter="updateHoverState(true)" @mouseleave="updateHoverState(false)">
    <slot>
      リンク先を指定してください
    </slot>
  </a>
</template>

<script>
export default {
  name: 'LinkButton',
  props: {
    to: {
      type: String,
      required: true
    },
    styleObject: {
      type: Object,
      default: function() {
        return this.defaultStyle
      }
    }
  },

  data() {
    return {
      hoverState: false,
      defaultStyle: {
        color: '#1a48d8',
        colorHover: '#fff',
        borderColor: '#1a48d8',
        borderColorHover: '#fff',
        backgroundColor: '#fff',
        backgroundColorHover: '#1a48d8'
      }
    }
  },
  computed: {
    styles() {
      let modifier = ''
      if (this.hoverState) modifier = 'Hover'

      const style = Object.assign(this.defaultStyle, this.styleObject)

      return {
        color: style['color' + modifier],
        'border-color': style['borderColor' + modifier],
        'background-color': style['backgroundColor' + modifier]
      }
    }
  },
  methods: {
    updateHoverState(isHover) {
      this.hoverState = isHover
    }
  }
}
</script>

<style lang="scss" scoped>
.link_button {
  display: inline-block;
  padding: 14px 70px;
  border: 1px solid;
  border-radius: 30px;
  text-decoration: none;
  &:hover {
    transition: 0.5s;
  }
}
</style>
