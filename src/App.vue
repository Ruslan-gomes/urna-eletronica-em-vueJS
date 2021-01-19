<template>
  <div id="app">

    <div class="urna">

      <tela
       :tela="tela"
       :numeroVoto="numeroVoto"
       :quantidadeNumeros="quantidadeNumeros"
       :candidato="candidato"
      />

      <teclado 
      :adicionarNumero="adicionarNumero"
      :corrigir="corrigir"
      :confirmar="confirmar"
      :votoBranco="votoBranco"
      />

    </div>
  </div>
</template>

<script>

import '@/style/global.css'
import teclado from './components/teclado.vue'
import tela from './components/tela.vue'

//importando os arquivos de audio das teclas
import keyAudio from './assets/audios/key.wav'
import confirmAudio from './assets/audios/confirm.wav'

export default {
  name: 'App',
  components: {
    teclado,
    tela
  },

  methods : {
    adicionarNumero: function(numero){
      //executa som das teclas
      this.executarSom(keyAudio);

      //verifica o limite de números digitados
      if(this.numeroVoto.length == this.quantidadeNumeros){
        return false;
      }
      //adiciona o número selecionado
      this.numeroVoto += '' + numero;

      //verifica candidato votado
      this.verificarCandidato();
    },

    verificarCandidato: function(){
      if(this.numeroVoto.length < this.quantidadeNumeros){
        return false;
      }
      if(this.candidatos[this.tela][this.numeroVoto]){
        this.candidato = this.candidatos[this.tela][this.numeroVoto];
        return true;
      }

      //voto nulo
      this.candidato = {
        nome: 'voto nulo',
        partido: 'voto nulo',
        imagem: ''
      }
    },
    corrigir: function(){
      this.executarSom(keyAudio);
      this.limpar();
    },

    limpar: function(){
      this.candidato = {};
      this.numeroVoto = '';
    },
    confirmar: function(){
       if(this.numeroVoto.length < this.quantidadeNumeros){
        return false;
      }

      return this.avancarTela();
    },
    avancarTela: function(){
      //executa som de confirmação
      this.executarSom(confirmAudio);

      if(this.tela == 'prefeito'){
        this.tela = 'vereador';
        this.quantidadeNumeros = 5;
        return this.limpar();
      }

      this.tela = 'fim';

      var instancia = this;

      setTimeout(function(){
        instancia.tela = 'prefeito';
        instancia.quantidadeNumeros = 2;
        instancia.limpar();
      } ,3000);
    },
    votoBranco: function(){
      if(this.tela == 'fim') {
        return false;
      }
      this.limpar();
      this.avancarTela();
    },
    executarSom: function(arquivoSom){
      if(arquivoSom){
        let audio = new Audio(arquivoSom)
        audio.play();
      }
    }
  },

  data(){
    return {
      tela: 'prefeito',
      numeroVoto: '',
      quantidadeNumeros: 2,
      candidato: {},
      candidatos: {
        "prefeito":{
          "01":{
            "nome": "Ash",
            "partido": "Pokemon",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/ash.png"
          },
          "08":{
            "nome": "Vegeta",
            "partido": "Dragon Ball",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png"
          }
        },
        "vereador":{
          "01234":{
            "nome": "Pikachu",
            "partido": "Pokemon",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/pikachu.png"
          },
          "08001":{
            "nome": "Goku",
            "partido": "Dragon Ball",
            "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/goku.png"
          }
        }
      }
    }
  }
}
</script>

<style>
#app {
  background-color: var(--background-color);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.urna{
  width: 900px;
  height: 500px;
  background-color: var(--ballot-box-background-color);
  padding: 20px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
}
</style>
