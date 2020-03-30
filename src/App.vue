<template>
  <div id="app">
    <Layout>
      <template v-slot:header>
        <div class="header__tags tags">
          <Tag
            v-for="(tag, value, index) in categories"
            :bgColor="tag.bgColor"
            :category="value"
            :isActive="tag.isActive"
            @togglePost="togglePost(value)"
            :key="index"
          >
            {{ tag.title }}
          </Tag>
        </div>
      </template>

      <template v-slot:posts>
        <div v-if="!isLoadPost" class="preloader__wrapper">
          <Preloader :width="90" :height="90" />
        </div>

        <transition name="posts">
          <div v-if="isLoadPost" class="posts__list" :style="{height: heightBox}">
            <Post
              v-for="post in posts"
              :key="post.id"
              :id="post.id"
              :size="post.size"
              :img="post.img"
              :tags="getTags(post.tags)"
              :title="post.title"
              :caption="post.caption"
              :link="post.link"
              :isBg="post.isBg"
              :isBtn="post.isBtn"
              :left="post.left"
              :top="post.top" />
          </div>
        </transition>

      </template>
    </Layout>
  </div>
</template>

<script>
import Layout from './layouts/Default.vue'
import Tag from './components/Tag.vue'
import Post from './components/Post.vue'
import Preloader from './components/Preloader.vue'
import img1 from './assets/img/1004-300x300.jpg'
import img2 from './assets/img/102-300x300.jpg'
import img3 from './assets/img/104-300x300.jpg'
import img4 from './assets/img/1047-300x300.jpg'
import img5 from './assets/img/1044-300x300.jpg'
import img6 from './assets/img/1048-300x300.jpg'
import img7 from './assets/img/1060-300x300.jpg'

export default {
  name: 'App',
  components: { Layout, Tag, Post, Preloader },
  data () {
    return {
      categories: {
        travel:{
          title: 'Travel',
          bgColor: 'bluish-purple--bg-color',
          isActive: true,
          category: 'travel'
        },
        explorers: {
          title: 'Explorers',
          bgColor: 'dull-orange--bg-color',
          isActive: true,
          category: 'explorers'
        },
        nature: {
          title: 'Nature',
          bgColor: 'greenish--bg-color',
          isActive: true,
          category: 'nature'
        },
        farming: {
          title: 'Сельское хозяйство',
          bgColor: 'greenish--bg-color',
          isActive: false,
          category: 'farming'
        },
        stern: {
          title: 'Корма',
          bgColor: 'dull-orange--bg-color',
          isActive: false,
          category: 'stern'
        },
        science: {
          title: 'Science',
          bgColor: 'cerulean--bg-color',
          isActive: true,
          category: 'science'
        }
      },
      posts:[
        {
          id: 1,
          size: [1, 1],
          img: img1,
          tags: 'travel',
          title: 'Robot’s Penguin Disguise Keeps Birds',
          caption: 'Figuring out how our brains work is key to understanding sdfsdf sdasd asd asasdasdas',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 2,
          size: [2, 1],
          img: img2,
          tags: 'explorers',
          title: '5 Things We Learned From X-Men: Days of Future Past',
          caption: 'Peter Dinklage’s porn ‘tache, Jennifer Lawrence’s brilliance and more. Some (tiny) spoilers ahead',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 3,
          size: [1, 1],
          img: '',
          tags: 'science',
          title: '14 Things Men Should Never Wear After 30',
          caption: 'Light a bonfire in the garden, and step bravely into your best-dressed decade',
          link: 'https://ya.ru',
          isBg: true,
          isBtn: true
        },
        {
          id: 4,
          size: [1, 1],
          img: '',
          tags: 'farming, stern',
          title: 'Комбикорма для уток и свиней оптом',
          caption: 'Наши корма дают +20% к приросту массы в год',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },

        {
          id: 5,
          size: [1, 1],
          img: img3,
          tags: 'explorers',
          title: 'Stunning Changes Along Colorado River',
          caption: 'Lake Powell offering kayakers new channels to explore',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 6,
          size: [1, 2],
          img: '',
          tags: 'travel',
          title: '14 Things Men Should Never Wear After 30',
          caption: 'Light a bonfire in the garden, and step bravely into your best-dressed decade',
          link: 'https://ya.ru',
          isBg: true,
          isBtn: true
        },
        {
          id: 7,
          size: [1, 1],
          img: img4,
          tags: 'nature',
          title: 'Offbeat Portraits Give Stars a New Turn',
          caption: 'Offbeat Portraits Give Stars a New Turn',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 8,
          size: [1, 1],
          img: img5,
          tags: 'explorers',
          title: 'Must See Places of the New Year',
          caption: 'Whether it’s India’s literary hub or mountain majesty',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 9,
          size: [1, 1],
          img: img6,
          tags: 'science',
          title: 'Robot’s Penguin Disguise Keeps Birds',
          caption: 'Figuring out how our brains work is key to understanding',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
        {
          id: 10,
          size: [1, 1],
          img: img7,
          tags: 'travel',
          title: 'Stunning Video Reveals Invisible CO2',
          caption: 'A NASA visualization shows the swirling gas',
          link: 'https://ya.ru',
          isBg: false,
          isBtn: false
        },
      ],
      matrix: {},
      cntCol: 4,
      heightBox: '1000px',
      isLoadPost: false
    }
  },

  mounted () {
    this.onResizeWindow()

    window.addEventListener('resize', this.onResizeWindow.bind(this))

    setTimeout(() => (this.isLoadPost = true), 1000)
  },

  beforeDestroy () {
    window.removeEventListener('resize', this.onResizeWindow.bind(this))
  },

  methods: {
    togglePost (val) {
      this.categories[val].isActive = !this.categories[val].isActive
      this.render();
    },

    getTags (tags) {
      return tags.split(',').map(tag => this.categories[tag.trim()])
    },

    isActive (tags) {
      return !!this.getTags(tags).find(item => item.isActive)
    },

    onResizeWindow () {
      this.updateCols()
      this.render()
    },

    updateCols () {
      const width = document.documentElement.clientWidth

      if (width > 1050) {
        this.cntCol = 4
      } else if (width > 800) {
        this.cntCol = 3
      } else {
        this.cntCol = 2
      }
    },

    maxSize (size) {
      return Math.min(size, 2)
    },

    render () {
      this.matrix = {}

      let colCnt = this.cntCol || 4

      let postX = 1
      let postY = 1

      let sizePaddTop = 320
      let sizePaddLeft = 250

      const setMatrixPlace = i => {
        if (postX > 4) {
          postX = 1;
          postY += 1;
        }

        let posMatrixX = postX;
        let posMatrixY = postY;

        for (let j = 0; j < this.posts[i].size[0]; j++) {
          posMatrixX += j;

          if (posMatrixX <= colCnt) {
            for (let k = 0; k < this.posts[i].size[1]; k++) {
              posMatrixY += k

              let matrixKey = `${posMatrixX}${posMatrixY}`

              if (this.matrix[matrixKey]) {
                postX +=1
                setMatrixPlace(i)
              } else {
                this.matrix[matrixKey] = true
              }
            }
          } else {
            postX = 1
            postY += 1

            setMatrixPlace(i)
          }
        }
      }

      for (let i = 0; i < this.posts.length; i++) {
        this.posts[i].size[0] = this.maxSize(this.posts[i].size[0])
        this.posts[i].size[1] = this.maxSize(this.posts[i].size[1])

        if (this.isActive(this.posts[i].tags)) {
          setMatrixPlace(i)

          this.posts[i].top = (postY - 1) * sizePaddTop + 'px'
          this.posts[i].left = (postX - 1) * sizePaddLeft + 'px'

          postX = postX + this.posts[i].size[0]
        }

      }

      this.heightBox = (postY + 1) * sizePaddTop + 'px'
    }
  }
}
</script>

<style lang="scss">
  .posts {
    &-enter-active {
      animation: posts-in .8s;
    }

    &-leave-active {
      animation: posts-in .8s reverse;
    }
  }

  .header__tags {
    display: flex;
    flex-wrap: wrap;
  }

  .preloader__wrapper {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .posts {
    padding: 5px 10px;

    &__list {
      position: relative;
      width: 100%;
      height: 940px;
    }
  }

  @keyframes posts-in {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
