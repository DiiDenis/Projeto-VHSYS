<template>
  <section 
    :style="{background: corFundo}"
    :class="{'padding': paddingArea}"
    v-bind="$props" >
    <slot />
  </section>
</template>

<script>
export default {
  name: 'SectionArea',
  provide: function () {
    return {
      nomeArea: this.nomeLocalizacao
    };
  },
  props: {
    nomeLocalizacao: {
      type: String,
      default: ''
    },
    corFundo: {
      type: String,
      default: ''
    },
    paddingArea:{
      type: Boolean,
      default: true
    }
  }
}
</script>

<style lang="scss" scoped>
  section{
    &.padding{
      padding-top: 48px;
      padding-bottom: 48px;
    }
  }
</style>