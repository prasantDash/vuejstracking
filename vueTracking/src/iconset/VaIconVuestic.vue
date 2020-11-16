<template src="./VaIconVuestic.html"></template>
<script>

  export default {
    name: 'VaIconVuestic',
    inject: ['contextConfig'],
    computed: {
      themeGradientId () {
        return this.contextConfig.invertedColor ? 'CORPORATE' : 'ORIGINAL'
      },
      textColor () {
        return this.contextConfig.invertedColor ? '#6E85E8' : '#E4FF32'
      },
    },
  }
</script>

<style lang="scss">
.va-icon-vuestic {
  .st0 {
    fill: #4ae387;
  }
}
</style>
