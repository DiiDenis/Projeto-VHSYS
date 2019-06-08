<template>
  <div class="section flex-align-center">
    <div class="container">
      <img :src="logo" alt="">
      <div class="float-right flex-align-center">
        <div class="contato mr15">
          <span>Fale conosco </span><strong>{{faleConosco}}</strong>
        </div>
        <div class="contato mr15">
          <span>WhatsApp </span><strong>{{whatsApp}}</strong>
        </div>
        <botao-primario 
          texto="Nós Ligamos" 
          tema="medium-dark-blue-stroke-theme"
          :on-click="() => console.log('teste')" />
        
      </div>
    </div>
  </div>
</template>

<script>

import Logo from '~/assets/img/logo.jpg'
import BotaoPrimario from '~/components/BotaoPrimario'

export default {
  name: 'HeaderPages',
  components: {
    Logo,
    BotaoPrimario
  },
  props: {
    tema: {
      type: String,
      default: 'nav-transparent-theme'
    },
    visibleBarraNavegacao : {
      type: Boolean,
      default: true,
    },
    faleConosco: {
      type: String,
      required: true
    },
    whatsApp: {
     type: String,
      required: true
    },
  },
  data(){
    return {
      logo: ''
    }
  },
  mounted: function () {
    this.logo = Logo
  },
  methods: {
   
  }
}
</script>

<style lang="scss" scoped>
  @import './assets/css/paleta';
  .section{
    width: 100%;
    display: block;
    min-height: 60px; 
  }
  .flex-align-center{
    display: flex;
    align-items: center;
  }
  .contato{
    margin-right: 20px;
    span{
      color: $medium-neutral;
      margin-right: 10px;
    }
    strong{
      font-size: 18px;
      color: $medium-dark-blue;
      position: relative;
      top: 3px;
    }
  }
</style>
