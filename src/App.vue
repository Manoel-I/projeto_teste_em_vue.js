<template>
  <div id="app">
    <h3> Cadastro: </h3>
    <small id="errorName" v-show="erroNome" >nome vazio ou invalido</small><br>
    <input type="text" placeholder="nome" v-model="nomeFild"><br>
    <input type="email" placeholder="email" v-model="emailFild"><br>
    <input type="number" placeholder="idade" v-model="idadeFild"><br>
    <button @click="cadastrarUsuario()" >Cadastrar</button>


    <div v-for="(cliente, index) in orderClientes " :key="cliente.id">
      <h4>{{index + 1}}</h4>  
      <Cliente_comp :cliente="cliente" @meDelete="deleteUsuario($event)"/> <!--@meDelete = chamando / "deleteUsuario" = escutando  -->
    </div>                                                                  <!-- o parametro $event recebe o que é enviado pelo $emit -->
  </div> 

</template>

<script>
//importação do componente
import Cliente_comp from "./components/Cliente_comp";
import _ from "lodash";
export default {
  name: 'App',
  data(){
    return{
      erroNome : false,
      nomeFild : '',
      emailFild : '',
      idadeFild : 0,

      clientes: [
        {
          id : 1,
          nome : "manoel",
          email : "manoel@gmail.com",
          idade : 24
        },
        {
          id : 2,
          nome : "marcos",
          email : "marcos@gmail.com",
          idade : 89
        },
        {
          id : 3,
          nome : "mauricio",
          email : "mauricio@gmail.com",
          idade : 67
        }
      ]
    }
  },
  components:{
    Cliente_comp,
  },
  methods:{
    cadastrarUsuario: function(){
      if(this.nomeFild == '' || this.nomeFild == ' ' || this.nomeFild.length < 2){
        console.log(this.erroNome);
        this.erroNome = true;
      }else{
        this.clientes.push({
          nome : this.nomeFild,
          email : this.emailFild,
          idade : this.idadeFild,
          id :  Date.now()
        });
      this.nomeFild = "";
      this.emailFild = "";
      this.idadeFild = 0;
      this.erroNome = false;
      } 
    },
    deleteUsuario: function($event){ //o $event é o que é recebido atraves do metodo no componente filho
      let id = $event.idCliente;
      let novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }
  },
  computed:{
    orderClientes: function(){
        return _.orderBy(this.clientes, ['nome'], ['asc']);
    }
  }
  
}
</script>

<style>
#errorName{
  color : red;
}

</style>
