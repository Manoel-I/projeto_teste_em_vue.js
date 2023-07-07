<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium' : isPremium}">
        <h4>Nome : {{ uppercaseFilter}}</h4>
        <hr>
        <p>Email : {{cliente.email}}</p>
        <p>Idade : {{cliente.idade}}</p>
        <p>ID : {{cliente.id}}</p>
        <button @click="mudarCor($event)">Mudar Cor</button>
        <button @click="meDelete()">Deletar</button>
    </div>
</template>

<script>
export default {
    data(){
        return {
            isPremium : false
        }
    }, 
    props: {
        cliente : Object,
    },
    methods:{
        mudarCor: function($event){
            console.log($event);
            this.isPremium = !this.isPremium;
        }, 
        meDelete: function(){
            console.log(this);
            this.$emit("meDelete",{idCliente : this.cliente.id}); // $emit = emitir / então aqui estamos emitindo o metodo "meDelete"
        }
    },
    computed: { // filters foram descontinuados, agora o cumputed que tem a mesma função - / eles não mudam o valor só a exibição
        uppercaseFilter(){
            console.log( this.cliente.nome);
            return this.cliente.nome.toUpperCase();
        }
    }
}


</script>


<style>
.cliente{
    background-color : #ECE5E3;
    max-width : 600px;
    height : 180px;
    padding : 1%;
    margin-top : 2%;
}

.cliente-premium{
    background-color : black;
    color : yellow;
    max-width : 600px;
    height : 180px;
    padding : 1%;
    margin-top : 2%;

}

</style>