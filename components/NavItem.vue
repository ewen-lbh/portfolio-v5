<template lang="pug">
component.--nav-item(
  :is="to ? 'nuxt-link' : 'span'"
  :to="to ? localePath(to) : false"
  :class="{current: to && isCurrent(to), 'has-a-click-handler': hasAClickHandler}"
  @click="$emit('click')"
): slot
</template>

<script>
export default {
  props: {
    to: {
      type: String,
      default: null
    }
  },
  computed: {
    hasAClickHandler() {
      return Object.keys(this.$listeners).includes('click')
    }
  },
  methods: {
    isCurrent(link) {
      if (process.browser) {
        const topPathFragment = this.$route.path
          .replace('fr/', '')
          .split('/')[1]
        if (!link.startsWith('/')) link = '/' + link
        return '/' + topPathFragment === link
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
.--nav-item
  text-transform uppercase
  border-bottom 1px solid transparent

.current
  border-bottom-color black

.has-a-click-handler
  cursor pointer
</style>
