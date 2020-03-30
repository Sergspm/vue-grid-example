<template>
  <button class="header__tags-item tag" :class="[ isActive && 'active', bgColor]" @click="$emit('togglePost')">
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    bgColor: {
      type: String,
      default: "white--color"
    },
    isActive: {
      type: Boolean,
      default: false,
    },
    category: {
      type: String,
      required: true
    }
  },
}
</script>

<style lang="scss">
  .header {
    &__tags-item{
      margin-right: 15px;
      margin-bottom: 5px;
      opacity: 0.5;
      cursor: pointer;
      transition: opacity 0.35s;

      &.active {
        opacity: 1;
      }

      &:hover {
        opacity: 0.7;
      }
    }
  }
</style>

