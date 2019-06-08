<template>
  <div :class="['inlineBlockButton', {flexButton: isFlex}]">
    <div 
      v-if="badge"      
      class="badge"
      @click="processarClique">
      {{ badge }}
    </div>
    <button 
      v-bind="$attrs"
      :class="[tema, tamanho]"
      class="botao-primario" 
      @click="processarClique">
      {{ texto }}
    </button>
  </div>
</template>

<script>

export default {
  name: 'BotaoPrimario',
  inheritAttrs: false,
  props: {
    texto: {
      type: String,
      required: true
    },
    tema: {
      type: String,
      default: 'dark-blue-filled-theme'
    },
    onClick: {
      type: Function,
      required: true
    },
    isFlex: {
      type: Boolean,
      default: true
    },
    badge: {
      type: String,
      default: ''
    },
    tamanho: {
      type: String,
      default: 'medium'
    },
    naoTrackearEvento: {
      type: Boolean,
      default: false,
    }
  },
  inject: {
    nomeArea: {
      default: ''
    }
  },
  methods: {
    processarClique: function (event) {
      // Aqui pode ser utilizado algo para trackear o click
      if (this.onClick && typeof this.onClick === 'function') {
        this.onClick(event, this.nomeArea)
      }
    },
  }
}
</script>

<style lang="scss" scoped>
  @import './assets/css/temas';

  .botao-primario {
      border-radius: 50px;
      text-align: center;
      display: flex;
      align-items: center;
      justify-content: center;
      min-width: 100px;
      width: 100%;
      cursor: pointer;
      transition: all 0.2s;
      user-select: none;
      font-weight: 700;
      letter-spacing: 1px;
      text-transform: uppercase;

      &:focus {
        outline: none;
      }
  }

  .flexButton {
    display: flex !important;
  }

  .inlineBlockButton {
    display: inline-block;
  }

  .badge {
    color: #FFF;
    background-color: $color-badge;
    border-radius: 4px; 
    position: absolute;
    right: 0px;
    top: -10px;
    padding: 6px;
    cursor: pointer;
    font-weight: normal;
  }

  .medium {
    height: 40px;
    font-size: 14px;
    padding: 0 20px 0 20px;
  }

  .big {
    height: 56px;
    font-size: 16px;
    padding: 0 32px 0 32px;
  }
</style>