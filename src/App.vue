<template>
  <div id="app">
    <h3>Cadastro:</h3>
    <small id="nomeErro" v-show="deuErro">O nome é inválido, tente novamente.</small><br />
    <input type="text" placeholder="nome" v-model="nomeField" /><br />
    <input type="email" placeholder="email" v-model="emailField" /><br />
    <input type="number" placeholder="idade" v-model="idadeField" /><br />
    <button @click="cadastrarUsuario">Cadastrar</button>
        <div class="buttons">
          <button class="button is-primary">Primary</button>
          <button class="button is-link">Link</button>
        </div>
    <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <hr />
      <h4>{{ index + 1 }}</h4>
      <Cliente
        :cliente="cliente"
        :showIdade="true"
        @meDelete="deletarUsuario($event)"
      />
      <h4>Edição</h4>
      <input type="text" v-model="cliente.nome" />
    </div>
    <hr />
  </div>
</template>

<script>
import _ from "lodash";
import Cliente from "./components/Cliente";

export default {
  name: "App",
  data() {
    return {
      deuErro: false,
      nomeField: "",
      emailField: "",
      idadeField: 0,
      clientes: [],
    };
  },
  components: {
    Cliente,
  },
  methods: {
    cadastrarUsuario: function () {
      if (
        this.nomeField == "" ||
        this.nomeField == " " ||
        this.nomeField.length < 3
      ) {
        this.deuErro = true;
      } else {
        this.deuErro = false;
        this.clientes.push({
          nome: this.nomeField,
          email: this.emailField,
          idade: this.idadeField,
          id: Date.now(),
        });
        this.nomeField = "";
        this.emailField = "";
        this.idadeField = 0;
      }
    },
    deletarUsuario: function ($event) {
      var id = $event.idDoCliente;
      //$event.component.testar();
      var novoArray = this.clientes.filter((cliente) => cliente.id != id);
      this.clientes = novoArray;
    },
  },
  computed: {
    orderClientes: function () {
      return _.orderBy(this.clientes, ["nome"], ["ASC"]);
    },
  },
};
</script>

<style>
#nomeErro {
  color: red;
}
</style>
