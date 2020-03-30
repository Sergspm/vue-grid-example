<template>
  <transition name="post">
    <div
      v-if="isActive(tags)"
      class="post__item"
      :class="[
        'post-' + id,
        'post--col-' + maxSize(size[0]),
        'post--row-' + maxSize(size[1]),
        {'post--bg': isBg},
        !img && 'post--no-image',
        size[0] > 1 && 'post--col']"
      :style="{ top: top, left: left }">

        <a
          :href="link"
          class="post__inner"
          :class="[isBg && tags[0].bgColor]"
        >
          <div
            v-if="img"
            class="post__img"
            :style="{ backgroundImage: 'url(' + img + ')' }">
          </div>

          <!-- Контент -->
          <div class="post__content">
            <!-- Теги -->
            <div class="post__tags">
              <div v-for="(tag, index) in tags" :key="index">
                <div
                  class="post__tag tag"
                  :class="tag.bgColor">
                  {{tag.title}}
                </div>
              </div>
            </div>
            <div class="post__title">
              {{title}}
            </div>
            <div class="post__text">
              {{title}}
            </div>
            <div v-if="isBtn" class="post__btn">
              Read more
            </div>
          </div>
        </a>
    </div>
  </transition>

</template>

<script>
export default {
  props: {
    id: {
      type: Number,
    },
    size: {
      type: Array,
      default: [1, 1]
    },
    img: {
      type: String,
      default: ''
    },
    tags: {
      type: Array,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    caption: {
      type: String,
      required: true
    },
    link: {
      type: String,
      required: true
    },
    isBg: {
      type: Boolean,
      default: false
    },
    isBtn: {
      type: Boolean,
      default: false
    },
    top: {
      type: String,
      default: "0px",
    },
    left: {
      type: String,
      default: "0px",
    }
  },
  methods: {
    isActive (tags) {
      return !!tags.find(tag => tag.isActive)
    },

    maxSize(size){
      return Math.min(size, 2)
    }
  }
}
</script>

<style lang="scss">

  .post-enter-active {
    animation: post-in .5s;
  }
  .post-leave-active {
    animation: post-in .5s reverse;
  }
  @keyframes post-in {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  .post {
    &__item {
      position: absolute;
      left: 0;
      top: 0;
      width: 230px;
      height: 300px;
      cursor: pointer;
      transition: all 0.35s;

      &:hover {
        box-shadow: 0 0 8px 0 rgba(0, 0, 0, .25);
      }
    }
    &__inner {
      display: flex;
      flex-direction: column;
      position: relative;
      width: 100%;
      height: 100%;
      background: #fff;
      border-radius: 4px;
    }
    &__img {
      width: 230px;
      flex: 1 0 auto;
      background-position: 50%;
      background-size: cover;
      background-repeat: no-repeat;
      transition: all 0.5s;
    }
    &__tags {
      position: absolute;
      top: 20px;
      left: 0;
      right: 0;
      padding-left: 20px;
    }
    &__tag {
      margin-bottom: 5px;
    }
    &__content {
      padding: 24px 19px;
      overflow: hidden;
    }
    &__title {
      margin-bottom: 5px;
      font-family: 'Montserrat', sans-serif;
      font-size: 15px;
      font-weight: bold;
      color: #3b3d40;
    }
    &__text {
      color: #818a8c;
    }
    &__btn {
      display: inline-block;
      margin-top: 15px;
      padding: 10px 25px;
      border-radius: 20px;
      font-family: 'Montserrat', sans-serif;
      text-transform: uppercase;
      letter-spacing: 2px;
      font-size: 10px;
      border: 1px solid rgba(0,0,0,.2);
      color: #838d8f;
    }
    &--col-2 {
      width: 480px;
    }
    &--row-2 {
      height: 620px;
    }
  }
  // Широкие
  .post--col{
    .post{
      &__inner {
        flex-direction: row;
      }
      &__content {
        padding: 20px 10px 20px 22px;
      }
      &__tags {
        position: static;
        padding-left: 0;
        margin-bottom: 8px;
      }
      &__title {
        margin-bottom: 10px;
        font-size: 22px;
      }
      &__img {
        order: 2;
        flex: 0 0 200px;
        height: 100%;
      }
    }
  }
  // С фоном
  .post--bg{
    .post{
      &__inner {
        justify-content: center;
      }
      &__img {
        display: none;
      }
      &__tags {
        position: static;
        margin-bottom: 10px;
        padding-left: 0;
      }
      &__content {
        text-align: center;
        padding: 20px;
      }
      &__title {
        margin-bottom: 12px;
        color: #fff;
        font-size: 22px;
      }
      &__text {
        color: rgba(255,255,255, .6);
      }
      &__btn {
        border: 1px solid rgba(255,255,255,.2);
        color: #fff;
      }
    }
  }
  // Без картинки
  .post--no-image {
    .post {
      &__tags {
        position: static;
        padding-left: 0;
        margin-bottom: 8px;
      }
    }
  }
  .post--no-image.post--col{
    .post {
      &__inner {
        flex-direction: column;
      }
    }
  }
</style>
