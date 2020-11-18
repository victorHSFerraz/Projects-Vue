<template>
  <div class="home">
    <h1></h1>
    <button class="resultado">{{calculadoraDisplay}}</button>
    <br>
    {{ Acao }} {{ posicaoAtual }} {{ x }} {{ y }}
    <br>
    <button class="botao0" @click="alertaValor('0')">0</button>
    <button class="botao1" @click="alertaValor('1')">1</button>
    <button class="botao2" @click="alertaValor('2')">2</button>
    <button class="botao3" @click="alertaValor('3')">3</button>
    <button class="botao4" @click="alertaValor('4')">4</button>
    <br>
    <button class="botao5" @click="alertaValor('5')">5</button>
    <button class="botao6" @click="alertaValor('6')">6</button>
    <button class="botao7" @click="alertaValor('7')">7</button>
    <button class="botao8" @click="alertaValor('8')">8</button>
    <button class="botao9" @click="alertaValor('9')">9</button>
    <br>
    <button class="botao+" @click="proximaFuncao('soma')">+</button>
    <button class="botao-" @click="proximaFuncao('menos')">-</button>
    <button class="botaoX" @click="proximaFuncao('multiplicacao')">X</button>
    <button class="botao/" @click="proximaFuncao('divisao')"> / </button>
    <button class="botao%" @click="proximaFuncao('porcentagem')">%</button>
    <br>
    <button class="botaoC" @click="proximaFuncao('apagar')">C</button>
    <button class="botaoPonto" @click="alertaValor('.')">.</button>
    <button class="botao=" @click="proximaFuncao('igual')">=</button>
    <button class="botaoTeste" @click="salvarApi()">S</button>
    <br>
    <br>
    

    

  </div>
</template>

<style lang="scss" scoped>

h1 {
  font-size: 40px;
}

button {
  background-color: rgb(0, 0, 0);
  border: 5px solid rgb(56, 52, 52);
  color:rgb(189, 185, 182);
  padding: 20px 30px;
  border-radius: 15px;
  text-align: center;
  font-size: 30px;
  margin: 3px 3px;
  cursor: pointer;
  width: 100px;
  
}
  button:hover{
    background-color: rgb(19, 18, 17);
    border: 5px solid rgb(228, 92, 1);
    color: rgb(250, 142, 0);
    text-shadow: 0 0 5px #f86707, 0 0 9px #e00d0d;
  } 
  

button.resultado {
  background-color: black;
  border: 5px solid rgb(63, 59, 59);
  width: 458px;
  height: 100px;
  border-radius: 15px;
  color: rgb(255, 255, 255);
  font-size: 50px;
  text-align: center;
  text-shadow: 0 0 5px #f86707, 0 0 9px #e00d0d;
}

</style>>

<script>
import Vue from 'vue'
import vueResource from 'vue-resource'
Vue.use(vueResource)
export default {
  data () {
    return {
      calculadoraDisplay : "",
      x: 0,
      y: 0,
      posicaoAtual : 1,
      Acao: 1
    }
  },
  mounted (){
    let request = this.$http.get('https://dev.api.amanet.com.br/v1/Operacao/')
    request.then(res => {
      console.log(res.data)
    })
  },
  methods:{
    salvarApi(){
      let request = this.$http.post('https://dev.api.amanet.com.br/v1/Calculadora/Calculo', {
	"Valor_x": Number(this.x),
	"Valor_y": Number(this.y),
	"Usuario_id": 221,
	"Operacao_id": this.Acao
})
      request.then(res => {
        console.log(res.data)
      })
      alert("Salvo com sucesso!")
   }, 
    alertaValor(valor){
      this.calculadoraDisplay = this.calculadoraDisplay+valor      
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
        }else if(this.posicaoAtual === 2){
          this.y = this.calculadoraDisplay
        }
    },
    proximaFuncao(valor){
      if(valor === 'soma'){
        this.Acao = 1
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
          this.posicaoAtual = 2
        }else{
          this.y = this.calculadoraDisplay
          this.posicaoAtual = 3
        }
        this.calculadoraDisplay = ""
      }else if(valor === 'igual') {
        if(this.Acao === 1) {
          this.calculadoraDisplay = Number(this.x) + Number(this.y)
          this.posicaoAtual = 1
        }
        else if(this.Acao === 2) {
          this.calculadoraDisplay = Number(this.x) - Number(this.y)
          this.posicaoAtual = 1
        }
        else if(this.Acao === 3) {
          this.calculadoraDisplay = Number(this.x) * Number(this.y)
          this.posicaoAtual = 1
        }
        else if(this.Acao === 4) {
          this.calculadoraDisplay = Number(this.x) / Number(this.y)
          this.posicaoAtual = 1
        } 
        else if(this.Acao === 5) {
          this.calculadoraDisplay = (Number(this.x) / 100) * Number(this.y)
          this.posicaoAtual = 1
        }
      }else if(valor === 'apagar') {
        this.x = 0
        this.y = 0
        this.calculadoraDisplay = ""
        this.posicaoAtual = 1
      }else if(valor === 'menos') {
        this.Acao = 2
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
          this.posicaoAtual = 2
        }else{
          this.y = this.calculadoraDisplay
          this.posicaoAtual = 3
        }
        this.calculadoraDisplay = ""
      }else if(valor === 'multiplicacao') {
        this.Acao = 3
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
          this.posicaoAtual = 2
        }else{
          this.y = this.calculadoraDisplay
          this.posicaoAtual = 3
        }
        this.calculadoraDisplay = ""
      }else if(valor === 'divisao') {
        this.Acao = 4
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
          this.posicaoAtual = 2
        }else{
          this.y = this.calculadoraDisplay
          this.posicaoAtual = 3
        }
        this.calculadoraDisplay = ""
      }else if(valor === 'porcentagem') {
        this.Acao = 5
        if(this.posicaoAtual === 1){
          this.x = this.calculadoraDisplay
          this.posicaoAtual = 2
        }else{
          this.y = this.calculadoraDisplay
          this.posicaoAtual = 3
        }
        this.calculadoraDisplay = ""
      }
    }
  }  
}
</script>
