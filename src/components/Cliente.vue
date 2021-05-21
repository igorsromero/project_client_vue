<template>
  <div :class="{ clientte: !isPremium, 'cliente-premium': isPremium }">
    <h4>Nome: {{ cliente.nome }}</h4>
    <p>{{ cliente.descricao }}</p>
    <p>Numero: {{ cliente.numero }}</p>
    <p>Email: {{ cliente.email | processarEmail }}</p>
    <p v-if="showIdade == true">Idade: {{ cliente.idade }}</p>
    <p v-else>O usuário escondeu a idade!</p>
    <button @click="mudarCor($event)">Mudar cor!</button>
    <button @click="emitirEventoDelete">Deletar</button>
    <h4>IDEspecial: {{idEspecial}}</h4>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPremium: false,
    };
  },
  props: {
    cliente: Object,
    showIdade: Boolean,
  },
  methods: {
    mudarCor: function ($event) {
      console.log($event);
      this.isPremium = !this.isPremium;
    },
    emitirEventoDelete: function () {
      //console.log("emitindo do filho");
      this.$emit("meDelete", {
        idDoCliente: this.cliente.id,
        curso: "Engenharia de Computação",
        emEstagio: true,
        component: this,
      });
    },
    testar: function(){
        alert("Isso é um alert!");
    }
  },
  filters:{
      processarEmail: function(value){
          return value.toUpperCase();
      }
  },
  computed:{
      idEspecial: function(){
          return (this.cliente.email + this.cliente.nome)
      }
  }
};
</script>

<style scoped>
.cliente {
  background-color: #ece5e3;
  color: black;
  padding: 1%;
  margin-top: 2%;
}

.cliente-premium {
  background-color: black;
  color: yellow;
  padding: 1%;
  margin-top: 2%;
}
</style>