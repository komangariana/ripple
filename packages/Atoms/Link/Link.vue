<template>
  <a v-if="!isNuxtLink" @focus="onFocus" class="rpl-link" :href="href" :target="linkTarget">
    <slot></slot>
  </a>
  <nuxt-link v-else @focus.native="onFocus" class="rpl-link rpl-link--nuxt" :to="href">
    <slot></slot>
  </nuxt-link>
</template>

<script>
import { focus } from 'vue-focus'
import { isRelativeUrl, isExternalUrl, isAnchorLink } from '@dpc-sdp/ripple-global/utils/helpers.js'

export default {
  name: 'RplLink',
  props: {
    href: String,
    target: { type: String, default: '' }
  },
  directives: {
    focus
  },
  data: function () {
    return {
      isNuxtLink: false,
      linkTarget: null
    }
  },
  methods: {
    onFocus: function (e) {
      this.$emit('focus', e)
    }
  },
  created: function () {
    if (!isAnchorLink(this.href) && isRelativeUrl(this.href)) {
      this.isNuxtLink = this.rplOptions.nuxt
    }
    // Set link target for non nuxt-links
    if (this.target.length === 0) {
      if (isExternalUrl(this.href, this.rplOptions.hostname)) {
        this.linkTarget = '_blank'
      }
    } else {
      this.linkTarget = this.target
    }
  }
}
</script>

<style lang="scss">
.rpl-link {
  text-decoration: none;

  &:hover,
  &:focus {
    text-decoration: underline;
  }
}
</style>
