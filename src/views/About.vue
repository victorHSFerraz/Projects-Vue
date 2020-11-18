<template>
  <div class="about">
    <table id="tabela" style="width:90%">
      <tr>
        <th>Id</th>
        <th>User Id</th>
        <th>Operação</th>
        <th>Valor X</th>
        <th>Valor Y</th>
        <th>Resultado</th>
        <th class="editar"></th>
        <th class="excluir"></th>
      </tr>
      <tr  v-for="(item, id) of listaNumeros" :key="id">
        <td>{{item.calculadora_id}}</td>
        <td>{{item.usuario_id}}</td>    
        <td>{{item.operacao_id}}</td>    
        <td>{{item.valor_x}}</td>    
        <td>{{item.valor_y}}</td>    
        <td>{{item.resultado}}</td> 
        <td class="editar"><button>Editar</button></td>
        <td class="excluir" @click="excluirOperacao(this.operacao_id)"><button>Excluir</button></td>   
    </tr>
    </table>
  </div>
</template>


<style>
table, th, td {
  border: 1px solid rgb(0, 0, 0);
  color: rgb(0, 0, 0);
  font-size: 20px;
}
th {
  background-color: #e2610b;
  color: white;
  height: 30px;
}
table {
  border-collapse: collapse;
}
tr:hover {background-color: #eee5e5;}
button {
  background-color: rgb(0, 0, 0);
  border: 1px white;
  color:rgb(255, 255, 255);
  padding: 10px 20px;
  text-align: center;
  font-size: 20px;
  margin: 3px 3px;
  cursor: pointer;
  width: 100px;
}
  button:hover{
    background-color: rgb(32, 31, 30);
  } 

  
</style>

<script>
import Vue from 'vue'
import vueResource from 'vue-resource'
Vue.use(vueResource)
export default {
  data (){
    return{
      listaNumeros:[]
    }
  },
  mounted (){
    let request = this.$http.get('https://dev.api.amanet.com.br/v1/Calculadora/HistoricoUsuario')
    request.then(res => {
      this.listaNumeros = res.data
    }) 
  },
  excluirOperacao (id){
    let request = this.$http.delete('https://dev.api.amanet.com.br/v1/Calculadora/HistoricoUsuario/'+id)
    request.then(res => {
      console.log(res.data)
    })
  },
}
</script>