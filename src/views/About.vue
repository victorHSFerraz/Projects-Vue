<template>
  <div class="about">
    <table id="tabela" style="width:100%">
      <tr class="info">
        <th>Id</th>
        <th>User Id</th>
        <th>Operação</th>
        <th>Valor X</th>
        <th>Valor Y</th>
        <th>Resultado</th>
        <th style="opacity:0; border:0; background-color: white"></th>
      </tr>
      <tr class="linhaValores" v-for="(item, id) of listaNumeros" :key="id">
        <td>{{item.calculadora_id}}</td>
        <td>{{item.usuario_id}}</td>    
        <td>{{item.operacao_id}}</td>    
        <td>{{item.valor_x}}</td>    
        <td>{{item.valor_y}}</td>    
        <td>{{item.resultado}}</td> 
        <td class="tdBotao" style="border: 0; background-color: white"><button class="btn-grad" @click="excluirOperacao(item.calculadora_id)">Excluir</button></td>   
    </tr>
    </table>
    <div class="oi">
    noffaaaa que tudo</div>
  </div>
</template>


<style lang="scss">
table, th, td {
  border: 1px solid rgb(0, 0, 0);
  color: rgb(0, 0, 0);
  font-size: 20px;
  width: 100px;
}
th {
  background-color: #e2610b;
  color: white;
  height: 30px;
  width: 200px;
}
table {
  border-collapse: collapse;
}
tr:hover {
  background-color: #eee5e5;
}
button {
  background-color: rgb(0, 0, 0);
  border: 1px white;
  color:rgb(255, 255, 255);
  padding: 10px 20px;
  text-align: center;
  font-size: 20px;
  margin: 3px 3px;
  cursor: pointer;
  width: 200px;  
  opacity:0;
  &:hover {
    background-color: rgb(32, 31, 30);
  }
}


.linhaValores{
  &:hover{
    button{
      opacity:1;
    }
  }
}

         
         .btn-grad {background-image: linear-gradient(to right, #FF512F 0%, #F09819  51%, #FF512F  100%)}
         .btn-grad {
            margin: 10px;
            padding: 15px 45px;
            text-align: center;
            text-transform: uppercase;
            transition: 0.5s;
            background-size: 200% auto;
            color: white;            
            box-shadow: 0 0 20px #eee;
            border-radius: 10px;
            display: block;
          }

          .btn-grad:hover {
            background-position: right center; /* change the direction of the change here */
            color: #fff;
            text-decoration: none;
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
  methods:{
    excluirOperacao (calculadora_id){
    let request = this.$http.delete('https://dev.api.amanet.com.br/v1/Calculadora/HistoricoUsuario/'+calculadora_id)
    request.then(res => {
      console.log(res.data)
      window.location.reload()
    })
    }
  }
}
</script>