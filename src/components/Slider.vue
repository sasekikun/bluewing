<template>
  <div ref="slider" class="slider">
    <div :style="sliderContainerStyles" class="slider_container">
      <ul v-for="n in 2" :style="barWidthStyle" :key="n" class="slider_bar">
        <li v-for="(image, index) in images" :key="index">
          <a v-if="image.link" :href="image.link">
            <img :src="image.url" :style="imagesStyles">
          </a>
          <img v-else :src="image.url" :style="imagesStyles">
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  props: {
    images: {
      type: Array,
      default: () => []
    },
    duration: {
      type: String,
      default: '12s'
    },
    imageWidth: {
      type: Number,
      default: 300
    },
    imageHeight: {
      type: Number,
      default: 300
    },
    imageMarginRight: {
      type: Number,
      default: 15
    }
  },
  data() {
    return {
      diffMargin: {
        type: Number,
        default: 0
      }
    }
  },
  computed: {
    barWidth() {
      return (this.imageWidth + this.imageMarginRight) * this.images.length
    },
    sliderContainerStyles() {
      return {
        'animation-duration': this.duration,
        width: `${(this.barWidth + this.diffMargin) * 2}px`
      }
    },
    barWidthStyle() {
      return {
        width: `${this.barWidth}px`,
        'margin-right': `${this.diffMargin}px`
      }
    },
    imagesStyles() {
      return {
        width: `${this.imageWidth}px`,
        height: `${this.imageHeight}px`,
        'margin-right': `${this.imageMarginRight}px`
      }
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      if (this.$refs.slider.clientWidth > this.barWidth) {
        this.diffMargin = this.$refs.slider.clientWidth - this.barWidth
      } else {
        this.diffMargin = 0
      }
    })
  }
}
</script>

<style lang="scss" scoped>
@keyframes slider {
  100% {
    transform: translateX(-50%);
  }
}

.slider {
  width: 100%;
  overflow: hidden;

  .slider_container {
    display: flex;
    animation-name: slider;
    animation-iteration-count: infinite;
    animation-timing-function: linear;

    .slider_bar {
      display: flex;
      list-style: none;
      margin: 0;
      padding: 0;

      li {
        a:hover {
          opacity: 0.6;
          transition: opacity 0.6s;
        }

        img {
          object-fit: cover;
          object-position: center;
        }
      }
    }
  }
}
</style>
