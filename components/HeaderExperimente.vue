<template>
  <section-area
    class="section-experimente-gratis"
    nome-localizacao="ExperimenteGratis">
    <div class="container">
      <div class="row">
        <div class="col-md-8 apresentacao">
            <h2>Sistema de Gestão Online Gratuito</h2>
            <h1><span>Experimente Grátis</span> por 7 dias</h1>  
            <strong>Sistema de gestão com pleto para pequenas e médias empresas</strong>
            <span>O VHSYS é o Sistema de Gestão Empresarial online que integra todas as áreas de sua empresa. Com ele você pode:</span>
            <div class="row beneficios">
            
              <div class="col-md-6">
                 <font-awesome-icon icon="fa-check" />
                <span>Emissão de notas fiscais eletronicas;</span>
                <span>Gestão de vendas e estoque;</span>
                <span>Controle financeiro;</span>
              </div>
              <div class="col-md-6">
                <span>Emissão de boletos;</span>
                <span>Orçamento de vendas;</span>
                <span>Integração contábil;</span>
              </div>
            </div>
        </div>
        <div class="col-md-4">
          <card-simples class="border-shadow">
            <div class="row-break">
              <strong>Digite seu e-mail</strong>             
              <base-input 
                v-model="email"
                :valid="(validacoes.email && email.length > 0)" 
                :error="(!validacoes.email && email.length > 0)"
                name="email"
                @input="emailValido(email)"/>           
            </div> 

            <div class="row-break">
              <strong>Seu nome completo</strong>             
              <base-input 
                v-model="nome"
                  :valid="(validacoes.nome)"
              :error="(nome.length > 0 && !validacoes.nome)"
                name="nomeCompleto"
                @input="validarNome(nome)"/>           
            </div> 

            <div class="row-break">
              <strong>Número do seu telefone</strong>             
              <base-input 
                v-model="telefone"
                :valid="(telefone.length == 14)"
                :error="(telefone.length > 0 && telefone.length < 14)" 
                name="telefone"
                string-mask="(##)#####-####"   
                @input="validarTelefone(telefone)"/>           
            </div> 

            <div 
              class="row-break">
              <strong>Já tem uma empresa formalizada?</strong>   
              <base-select 
                v-model="empresaFormalizada"
                :valid="(validacoes.empresaFormalizada && empresaFormalizadaIsTouched)"
                :error="(!validacoes.empresaFormalizada && empresaFormalizadaIsTouched)" 
                :options="empresaFormalizadaOption"  
                name="empresaFormalizada" 
                @input="validarEmpresaFormalizada()"/>       
            </div>

            <div class="row-break">
              <strong>Digite seu nome de usuário</strong>             
              <base-input 
                v-model="nomeUsuario"
                :valid="(validacoes.nomeUsuario && nomeUsuario.length > 0)" 
                :error="(!validacoes.nomeUsuario && nomeUsuario.length > 0)"
                name="nomeUsuario"
                @input="validarUser(nomeUsuario)"/>           
            </div> 

            <div class="row-break">
              <strong>Digite sua senha</strong>             
              <base-input 
                v-model="senha"
                :valid="(validacoes.senha && nomeUsuario.senha > 0)" 
                :error="(!validacoes.senha && nomeUsuario.senha > 0)"
                name="senha"
                @input="validarSenha(senha)"/>           
            </div> 

            <div class="row-breal">
               <botao-primario 
                texto="Experimente grátis" 
                tema="purple-accent-filled-theme-font-white"
                :on-click="() => console.log('teste')" />
            </div>
            <span class="observacao">Clicando no botão acima você concorda com nossos <a href="/">termos de uso</a></span>

          </card-simples>
        </div>
      </div>
    </div>
  </section-area>
</template>
<script>


import SectionArea from '~/components/SectionArea'
import CardSimples from '~/components/CardSimples'
import BaseInput from '~/components/BaseInput'
import BaseSelect from '~/components/BaseSelect'
import BotaoPrimario from '~/components/BotaoPrimario'


export default {
  name: 'ComoFuncionaContabilizei',
  components: {
    SectionArea,
    CardSimples,
    BaseInput,
    BaseSelect,
    BotaoPrimario
  },
  props: {
    botao: {
      type: Boolean,
      default: true
    },
    migracao:{
      type: Boolean,
      default: false
    },
    title:{
      type: String,
      default: 'AAA'
    },
    descricao:{
      type: String,
      default: 'VVV'
    }   
  },
  data(){
    return{
      logo: '',
      email: '',
      nome: '',
      telefone: '',
      empresaFormalizada:'',
      nomeUsuario: '',
      senha: '',
      empresaFormalizadaIsTouched: false,
      validacoes:{
        email: false,
        nome: false,
        telefone: false,
        empresaFormalizada: false,
        nomeUsuario: false,
        senha: false
      },
      empresaFormalizadaOption: [
        { text: 'Selecione uma opção', value: '' },
        { text: 'Sim', value: 'sim' },
        { text: 'Não', value: 'não' },
      ],
    }
  },
  mounted() {
    
  },
  methods: {
    emailValido: function (email) {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/    
      this.validacoes.email = re.test(email)
      return this.validacoes.email
    },
    validarNome: function (nome) {    
      const filter_nome = /^[A-Za-z]+([ ][A-Za-z]+)*$/;
      this.validacoes.nome =  filter_nome.test(nome) && this.nome.length > 3 
    },
    validarUser: function (nomeUsuario) {    
       const filter_user = /^[A-Za-z]+$/;
      this.validacoes.nomeUsuario =  filter_user.test(nomeUsuario) && this.nomeUsuario.length > 3 
    },
    validarTelefone: function () {      
      this.validacoes.telefone = this.telefone.length == 14      
    },
    validarSenha: function () {      
      this.validacoes.senha = this.senha.length > 7      
    },
    validarEmpresaFormalizada: function () {    
      this.validacoes.empresaFormalizada = this.empresaFormalizada !== ''
      this.empresaFormalizadaIsTouched = true
    },
  }
}
</script>

<style lang="scss" scoped>
  @import "./assets/css/paleta";

  .section-experimente-gratis {    
    background-size: cover;
    background-position: bottom;
    background-repeat: no-repeat;
    padding-top: 70px;
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    color: #fff;
    z-index: 1;
    position: relative;   
    background-image: url('../assets/img/background.png');
    height: 570px;
  }

  .row-break{
     display: block;
     width: 100%;
     margin-bottom: 55px;
   }

   .observacao{
     margin-top: 10px;
     display: inline-block;
     font-size: 11px;
     a{
       font-weight: bold;
       color: #34a95e;
     }
   }

   .apresentacao{
    h1{
       color: #fff;
       margin-bottom: 30px;
       span{
         color: #67ca6a;
       }
    }
    h2{
      color: #fff;
      margin-bottom: 30px;
      margin-top: 60px;
    }
     > strong{
      color: #efefef;
      font-size: 14px;
      display: block;
    }
    > span{
      color: #efefef;
      font-size: 14px
    }
    .beneficios{
      span{
        color: #fff;
      }
    }
   }

</style>
