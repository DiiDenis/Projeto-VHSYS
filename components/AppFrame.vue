<template>
  <!-- TODO: Cache components https://www.npmjs.com/package/@nuxtjs/component-cache -->
  <div>
    <header-app fale-conosco="0800 007 0017" whats-app="(41 99871-8914)" />
    <div class="">
      <slot/>
    </div>
    <section-area 
      :padding-area="false"
      nome-localizacao="Rodapé">
      <section>teste</section>
    </section-area>
  </div>
</template>

<script>

import SectionArea from '~/components/SectionArea'
import HeaderApp from '~/components/HeaderApp'
import { EXTRA_SMALL, SMALL, MEDIUM, LARGE, EXTRA_LARGE } from '~/assets/js/constantes/tamanhoTela'

export default {
  name: 'AppFrame',
  components: {
    SectionArea,
    HeaderApp
  },
  props: {
    tema: {
      type: String,
      default: 'nav-transparent-theme'
    },
    visibleBarraNavegacao : {
      type: Boolean,
      default: true,
    }
  },
  mounted: function () {
    const self = this
    self.setDevice(window.innerWidth)
    self.setScreenSize(window.innerWidth)
    window.addEventListener('resize', function() {
      self.setDevice(window.innerWidth)
      self.setScreenSize(window.innerWidth)
    }, { passive: true })
  },
  methods: {
    setDevice: function(windowWidth) {
      const isMobile = windowWidth < 992
      this.$nuxt.$emit('deviceType', isMobile)
    },
    setScreenSize: function(size) {
      const screenDevice = this.getScreenSize(size)
      this.$nuxt.$emit('deviceSize', screenDevice)
    },
    getScreenSize: function(windowWidth) {
      if (windowWidth >= 0 && windowWidth < 576) return EXTRA_SMALL
      if (windowWidth >= 576 && windowWidth < 768) return SMALL
      if (windowWidth >= 768 && windowWidth < 992) return MEDIUM
      if (windowWidth >= 992 && windowWidth < 1200) return LARGE
      else return EXTRA_LARGE
    }
  }
}
</script>

<style lang="scss" scoped>
.container-site{
  width: 1200px;
  margin: 0 auto;    
}
</style>
