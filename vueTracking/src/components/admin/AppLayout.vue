<template src="./AppLayout.html"></template>

<script>
import AppPageLayout from './AppPageLayout'
import AppNavbar from './app-navbar/AppNavbar'
import AppTopbar from './app-topbar/AppTopbar'
import AppSidebar from './app-sidebar/AppSidebar'
import { originalTheme, corporateTheme } from 'vuestic-ui/src/services/themes'
import {
  ColorThemeActionsMixin,
  ColorThemeMixin,
} from '../../services/vuestic-ui'

export default {
  name: 'app-layout',
  components: {
    AppPageLayout,
    AppNavbar,
    AppTopbar,
    AppSidebar,
  },
  data () {
    return {
      isTopBar: false,
      minimized: false,
      mobileWidth: 767,
    }
  },
  inject: ['contextConfig'],
  mixins: [ColorThemeActionsMixin, ColorThemeMixin],
  created () {
    if (this.$route.query && this.$route.query.theme === 'corporate') {
      this.setTheme('corporate')
    }
    this.$root.$on('change-theme', this.setTheme)
  },
  beforeDestroy () {
    this.$root.$off('change-theme', this.setTheme)
  },
  methods: {
    setTheme (themeName) {
      const theme = themeName === 'corporate' ? corporateTheme : originalTheme
      this.setColors(theme.colors)
      Object.keys(theme.context).forEach((key) => {
        this.contextConfig[key] = theme.context[key]
      })
    },
  },
}
</script>

<style lang="scss">
.app-layout {
  display: flex;
  flex-direction: column;

  &__container {
    display: flex;
    flex-wrap: nowrap;
    align-items: stretch;
    // TODO Probably there is a better way to achieve this.
    height: calc(100% - 65px);

    @include media-breakpoint-down(sm) {
      height: calc(100% - 110px);
    }
  }

  &__main {
    box-sizing: border-box;
    width: 100%;
    position: relative;
    max-height: 100%;
    min-height: 100%;

    &--top {
    }

    &-layout {
      position: absolute;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0;
      overflow: auto;
      box-sizing: border-box;
      min-height: 100%;
      margin: 0;
    }
  }
}
</style>
