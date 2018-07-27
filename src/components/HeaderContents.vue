<!--suppress ALL -->
<template>

  <div :class="changeLayout">

    <div id="images" :style="{textAlign:images.position}">
      <img :src="defaultImages.src" :alt="defaultImages.alt" :style="changeImageHeight">
    </div>

    <nav id="global_nav" :style="addMarginTop">
      <ul :class="changeMenuTextAlign" class="global_nav_list">
        <li v-for="(pcMenu, key) in pcMenus" :key="key">
          <a :href="pcMenu.to" :style="changePcTextColor">
            {{ pcMenu.title }}
          </a>

          <ul v-if="pcMenu.subMenus" class="global_nav_sub_list">
            <li v-for="(subMenu, key) in pcMenu.subMenus" :key="key">
              <a :href="subMenu.to" :style="changePcTextColor">
                {{ subMenu.title }}
              </a>
            </li>
          </ul>

        </li>
      </ul>
    </nav>

    <div class="sp_menu">

      <label class="toggle" for="open">
        <i :style="changeIconColor" class="fas fa-bars" />
      </label>
      <input id="open" type="checkbox">

      <div id="menu" :style="changeSpMenuBackground">
        <div :style="changeSpMenuTextColor" class="close_icon_wrapper">
          <h3>{{ defaultNavStyle.spMenuTitle }}</h3>
          <label for="open">
            <i class="fas fa-times close_icon"/>
          </label>
        </div>

        <nav>
          <div :style="changeSpMenuTextColor" class="sp_menu_list">
            <label v-for="(spMenu, key) in spMenus" :key="key">

              <div v-if="spMenu.subMenus" class="sp_sub_menu_wrapper">
                <input id="spMenu" type="checkbox" class="on-off">
                <label for="spMenu" class="menu-label">{{ spMenu.title }}</label>

                <ul v-if="spMenu.subMenus" class="sp_sub_menu_list">
                  <li v-for="(subMenu, key) in spMenu.subMenus" :key="key">
                    <a :href="spMenu.to" :style="changeSpMenuTextColor">
                      {{ subMenu.title }}
                    </a>
                  </li>
                </ul>

              </div>

              <div v-else class="sp_sub_menu_wrapper">
                <a :href="spMenu.to" :style="changeSpMenuTextColor">
                  {{ spMenu.title }}
                </a>
              </div>

            </label>
          </div>
        </nav>

      </div>

    </div>
  </div>

</template>

<script>
import '@fortawesome/fontawesome-free-webfonts/css/fontawesome.css'
import '@fortawesome/fontawesome-free-webfonts/css/fa-solid.css'

export default {
  name: 'HeaderContents',
  props: {
    images: {
      type: Object,
      default: function() {
        return {
          src: '../static/images/logo.png',
          alt: 'ロゴ画像',
          height: 80,
          position: ''
        }
      }
    },
    pcMenus: {
      type: Array,
      default: function() {
        return [
          {
            title: 'SampleNav',
            to: '/'
          },
          {
            title: 'SampleNav',
            to: '/',
            subMenus: [
              {
                title: 'SampleSubNav',
                to: '/'
              },
              {
                title: 'SampleSubNav',
                to: '/'
              }
            ]
          },
          {
            title: 'SampleNav',
            to: '/'
          }
        ]
      }
    },
    spMenus: {
      type: Array,
      default: function() {
        return [
          {
            title: 'SampleNav',
            to: '/'
          },
          {
            title: 'SampleNav',
            to: '',
            subMenus: [
              {
                title: 'SampleNav',
                to: '/'
              },
              {
                title: 'SampleSubNav',
                to: '/'
              },
              {
                title: 'SampleSubNav',
                to: '/'
              }
            ]
          },
          {
            title: 'SampleNav',
            to: '/'
          }
        ]
      }
    },
    navStyle: {
      type: Object,
      default: function() {
        return {
          pcMenuTextAlign: 'left',
          pcMenuTextColor: '#191b41',
          spMenuTitle: 'MENU',
          spMenuTextColor: '#fff',
          spIconColor: '#191b41',
          spMenuBackground: '#191b41',
          marginTop: 0,
          layout: ''
        }
      }
    }
  },
  data() {
    return {
      width: window.innerWidth,
      defaultImages: {
        src: '../static/images/logo.png',
        alt: 'ロゴ画像',
        height: 80,
        position: ''
      },
      defaultNavStyle: {
        pcMenuTextAlign: 'left',
        pcMenuTextColor: '#191b41',
        spMenuTitle: 'MENU',
        spMenuTextColor: '#fff',
        spIconColor: '#191b41',
        spMenuBackground: '#191b41',
        marginTop: 0,
        layout: ''
      }
    }
  },
  computed: {
    changeLayout() {
      return {
        center_layout:
          (this.pcMenus.length >= 4 && this.navStyle.layout === '') ||
          (this.pcMenus.length >= 4 && this.navStyle.layout === undefined) ||
          (this.pcMenus.length <= 3 && this.navStyle.layout === 'center') ||
          (this.pcMenus.length >= 4 && this.navStyle.layout === 'center'),
        right_layout:
          (this.pcMenus.length <= 3 && this.navStyle.layout === '') ||
          (this.pcMenus.length <= 3 && this.navStyle.layout === undefined) ||
          (this.pcMenus.length >= 4 && this.navStyle.layout === 'right') ||
          (this.pcMenus.length <= 3 && this.navStyle.layout === 'right')
      }
    },
    changeMenuTextAlign() {
      return {
        text_align_right: this.navStyle.pcMenuTextAlign === 'right',
        text_align_center: this.navStyle.pcMenuTextAlign === 'center',
        text_align_left:
          this.navStyle.pcMenuTextAlign === 'normal' ||
          this.navStyle.pcMenuTextAlign === undefined
      }
    },
    changeImageHeight() {
      const images = Object.assign(this.defaultImages, this.images)
      const displaySize = this.width
      if (displaySize <= 767) {
        return {
          width: '80%',
          height: 'auto'
        }
      } else {
        return {
          height: images['height'] + 'px'
        }
      }
    },
    changePcTextColor() {
      const style = Object.assign(this.defaultNavStyle, this.navStyle)
      return {
        color: style['pcMenuTextColor']
      }
    },
    changeIconColor() {
      const style = Object.assign(this.defaultNavStyle, this.navStyle)
      return {
        color: style['spIconColor']
      }
    },
    changeSpMenuBackground() {
      const style = Object.assign(this.defaultNavStyle, this.navStyle)
      return {
        backgroundColor: style['spMenuBackground']
      }
    },
    changeSpMenuTextColor() {
      const style = Object.assign(this.defaultNavStyle, this.navStyle)
      return {
        color: style['spMenuTextColor']
      }
    },
    addMarginTop() {
      const style = Object.assign(this.defaultNavStyle, this.navStyle)
      return {
        marginTop: style['marginTop'] + 'px'
      }
    }
  },
  created() {
    window.addEventListener('resize', this.setWindowWidth, false)
  },
  destroyed() {
    window.removeEventListener('resize', this.setWindowWidth, false)
  },
  methods: {
    setWindowWidth() {
      this.width = document.documentElement.clientWidth
    }
  }
}
</script>

<style lang="scss" scoped>
// global navigation scss
@mixin right_style {
  display: flex;
  align-items: center;
}

.center_layout {
  display: block;

  ul {
    justify-content: center;
  }

  @media screen and (max-width: 767px) {
    @include right_style;
  }
}

.right_layout {
  header {
    display: flex;
  }
  nav {
    margin-left: auto;
  }
  @include right_style;
  ul {
    margin-left: auto;
  }
}

.text_align_right {
  justify-content: flex-end;
}

.text_align_center {
  justify-content: center;
}

.text_align_left {
  justify-content: normal;
}

#global_nav {
  @media screen and (max-width: 767px) {
    display: none;
  }
}

.global_nav_list {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  padding: 0;
  margin: 0;
  cursor: pointer;

  li {
    position: relative;
    font-weight: bold;
    margin: 0 15px;
  }

  a {
    display: block;
    margin: 0;
    line-height: 1;
    text-decoration: none;
  }
}

.global_nav_sub_list {
  list-style: none;
  position: absolute;
  z-index: 3;
  top: 100%;
  left: 0;
  margin: 0;
  padding: 0;

  li {
    margin: 0;
    background: rgba(255, 255, 255, 0.6);
  }
}

// global navigation animation scss
.global_nav_sub_list {
  li {
    overflow: hidden;
    height: 0;
    transition: 0.2s;
    padding: 0 10px;
  }
}
.global_nav_list li:hover ul li {
  overflow: visible;
  height: 20px;
  padding: 10px 10px;
}

// hamburger menu scss
.sp_menu {
  display: none;

  @media screen and (max-width: 767px) {
    display: block;
    margin-left: auto;
  }
}

#menu {
  border-radius: 50px 0 0 50px;
  position: fixed;
  top: 0;
  right: -100%;
  width: 75%;
  height: 100%;
  transition: left 0.5s, right 0.5s;
  z-index: 3;
}

.toggle {
  font-size: 50px;
  cursor: pointer;
}

.toggle:hover {
  text-decoration: underline;
}

#open {
  display: none;
}

#open:checked + #menu {
  right: 0;
}

.close_icon_wrapper {
  display: flex;
  align-items: center;
  border-bottom: 1px dotted;
  margin: 20px 40px 0;

  h3 {
    width: 100%;
  }
}

.close_icon {
  font-size: 50px;
}

.sp_menu_list {
  padding: 0;
  margin-left: 40px;

  li {
    list-style: none;
    margin: 10px 0;
  }
  p {
    margin: 0;
  }

  a {
    text-decoration: none;
  }
}

.sp_sub_menu_wrapper {
  margin: 10px 0;

  a::before,
  label::before {
    font-family: 'Font Awesome 5 Free';
    content: '\f105';
    display: inline-block;
  }

  input {
    display: none;
  }
}
.menu-label::before {
  margin-right: 0.3em;
}

.sp_sub_menu_list {
  max-height: 0;
  overflow: hidden;
  transition: all 0.2s ease-out;
  margin: 0;
  padding-left: 30px;

  a::before {
    content: '-';
  }
}

.on-off:checked + label + .sp_sub_menu_list {
  max-height: 500px;
  transition: all 0.2s ease-in;
}
.on-off:checked + label::before {
  content: '\f107';
  font-weight: bold;
}
</style>
