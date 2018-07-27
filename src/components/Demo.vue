<template>
  <div>
    <Header :images="images" :pc-menus="pcMenus" :sp-menus="spMenus" :nav-style="navStyle"/>
    <HeadLine :text-color="'pink'" :font-size="'2em'" :text-align="'center'">NEWS!!!</HeadLine>
    <LinkButton :to="'/'" :style-object="styles">リンク</LinkButton>
    <Slider :images="sliderImages" :image-width="200" :image-margin-right="10" :duration="'9s'"/>
    <EyeCatch :height="400" :speed="0.6" src="http://gahag.net/img/201608/27s/gahag-0119446360-1.jpg"/>
    <FooterContents :logo-image="logo" :style-object="styleObject" :copy-right="'株式会社させきくん'"/>
  </div>
</template>

<script>
import HeaderContents from '@/components/HeaderContents'
import FooterContents from '@/components/FooterContents'
import Slider from '@/components/Slider'
import HeadLine from '@/components/HeadLine'
import LinkButton from '@/components/LinkButton'
import EyeCatch from './EyeCatch.vue'

export default {
  name: 'Demo',
  components: {
    Header: HeaderContents,
    FooterContents,
    LinkButton,
    Slider,
    HeadLine,
    EyeCatch
  },
  data: function() {
    return {
      styles: {
        color: '#00f',
        colorHover: '#0f0',
        backgroundColorHover: '#f00'
      },
      sliderImages: [
        {
          url: 'http://secrettalk.me/images/talk/8-9-bW90aGVyZmFybTQuanBn'
        },
        {
          url:
            'https://pbs.twimg.com/profile_images/416635739464429568/9L6YmwrT.jpeg'
        },
        {
          url:
            'https://pbs.twimg.com/profile_images/581025665727655936/9CnwZZ6j.jpg'
        }
      ],
      logo: {
        src: 'https://sasekikun.co.jp/images/logo_w.svg',
        height: '47px',
        alt: 'ロゴ'
      },
      styleObject: {
        textColor: '#ffd',
        backgroundColor: '#00bcd4'
      },
      images: {
        src: 'https://www.nettai.co.jp/wp-content/uploads/2013/09/dsc_4188.jpg',
        alt: 'これはロゴ画像',
        position: ''
      },
      navStyle: {
        pcMenuTextAlign: 'left',
        pcMenuTextColor: 'blue',
        spMenuTitle: 'SP MENU',
        spMenuTextColor: 'blue',
        spIconColor: 'skyblue',
        spMenuBackground: 'skyblue',
        marginTop: 40
      },
      pcMenus: [
        {
          title: 'HOME',
          to: '/'
        },
        {
          title: 'HOME',
          to: '/'
        },
        {
          title: 'HOME',
          to: '/'
        },
        {
          title: 'COMPANY',
          to: '/company',
          subMenus: [
            {
              title: 'concept',
              to: '/concept'
            },
            {
              title: 'hoge',
              to: 'http://www.google.com'
            }
          ]
        }
      ],
      spMenus: [
        {
          title: 'HOME',
          to: '/'
        },
        {
          title: 'COMPANY',
          to: '',
          subMenus: [
            {
              title: 'company',
              to: '/concept'
            },
            {
              title: 'concept',
              to: '/concept'
            },
            {
              title: 'hoge',
              to: '/hoge'
            }
          ]
        },
        {
          title: 'CONTACT',
          to: '/contact'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
footer {
  a {
    color: #ffc;
  }
  p {
    margin: 0;
  }
  address {
    padding: 1em;
  }
}
</style>
