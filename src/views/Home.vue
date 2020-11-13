<template>
  <div class="home">
    <h1>CALCULADORA</h1>
    <button class="resultado">123456789</button>
    <br>
    <button class="botao0">0</button>
    <button class="botao1">1</button>
    <button class="botao2">2</button>
    <button class="botao3">3</button>
    <button class="botao4">4</button>
    <br>
    <button class="botao5">5</button>
    <button class="botao6">6</button>
    <button class="botao7">7</button>
    <button class="botao8">8</button>
    <button class="botao9">9</button>
    <br>
    <button class="botao+">+</button>
    <button class="botao-">-</button>
    <button class="botaoX">X</button>
    <button class="botao/"> / </button>
    <button class="botao%">%</button>
    <br>
    <button class="botaoC">C</button>
    <button class="botao=">=</button>
    <button class="botaoSLEEP">SLEEP</button>
    <br>
    <br>
    

    

  </div>
</template>

<style scoped>

button {
  background-color: rgb(0, 0, 0);
  border: 5px solid rgb(63, 59, 59);
  color:rgb(231, 108, 7);
  padding: 20px 30px;
  text-align: center;
  font-size: 30px;
  margin: 3px 3px;
  cursor: pointer;
}
  button:hover{
    background-color: rgb(19, 18, 17);
    border: 5px solid rgb(228, 92, 1);
  } 
  

button.resultado {
  background-color: black;
  border: 5px solid rgb(63, 59, 59);
  width: 458px;
  height: 100px;
  color: rgb(255, 255, 255);
  font-size: 50px;
  text-align: center;
}

</style>>

<script>


export default {
  
}
</script>
