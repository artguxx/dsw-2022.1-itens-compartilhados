<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li><router-link class="link" :to="{ name: 'item-list' }">Itens Compartilhados</router-link></li>
          <li>Detalhes</li>
        </ol>
        <h2>Detalhes</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
         <div class="form-items-compartilhados row" v-if="this.$root.credentials">
          <div class="col-md-10 col-md-offset-1 text-left">
            <div>
              <div class="header">
                <h2 class="form-title">Detalhes de item compartilhado</h2>
                <h6 class="form-subtitle mx-3">Abaixo estão os detalhes do item compartilhado.</h6>
                <div class="">
                  <button type="button" style="float: right; background-color: #4154f1;" class="btn btn-primary" @click="abrirForm()">Novo Compartilhamento</button>
                </div>
              </div>
            </div>

            <div class="header">
              <h2 class="form-title h4">Nome</h2>
              <h6 class="form-subtitle mx-3">{{item.nome}}</h6>
              <h2 class="form-title h4">Descrição</h2>
              <h6 class="form-subtitle mx-3">{{item.descricao}}</h6>
              <h2 class="form-title h4">Tipo</h2>
              <h6 class="form-subtitle mx-3">{{item.tipo}}</h6>
            </div>

            <form class="form-inline" style="float: right" v-if="formAberto" @submit.prevent="cadastrar()">
              <div class="form-group">
                <label for="email">Email</label>
                <input type="text" class="form-control" id="email" placeholder="Email do usuário" v-model="form.emailUsuario">
              </div>

              <div class="form-group">
                <label for="dtInicio">Data Início</label>
                <input class="form-control" id="dtInicio" type="date" v-model="form.dataInicio">
              </div>

              <div class="form-group">
                <label for="dtTermino">Data Término</label>
                <input class="form-control" id="dtTermino" type="date" v-model="form.dataTermino">
              </div>

              <button type="submit" class="btn btn-primary">Cadastrar</button>
            </form>

            <div v-for="status of statusForm" style="float: right">{{status}}</div>

            <table class="table table-striped" id="tbItens">
              <thead>
                <tr>
                  <th>Data Início</th>
                  <th>Data Término</th>
                  <th>Usuário</th>
                  <th>Status</th>
                  <th class="commands"></th>
                </tr>
              </thead>

              <tbody>
                <tr v-for="compartilhamento in compartilhamentos">
                  <td>{{compartilhamento.dataInicio | readableDate}}</td>
                  <td>{{compartilhamento.dataTermino | readableDate}}</td>
                  <td>{{compartilhamento.nomeUsuario}}</td>
                  <td>{{compartilhamento.status}}</td>
                  <td class="commands">
                    <font-awesome-icon icon="fa-solid fa-ban" v-if="!compartilhamento.status.includes('CANCELADO')" aria-hidden="true" title="Cancelar" style="color: red" @click="confirma(compartilhamento)"/>
                    
                  </td>
                </tr>
              </tbody>
            </table>

            <div v-if="check">
              <span>Tem certeza que deseja cancelar este compartilhamento?</span>
              <button class="btn btn-danger" @click="remove(toRemove)">Sim</button>
            </div>
            <span class="error" v-if="error[toRemove.id]">{{error[toRemove.id]}}</span>
          </div>
        </div>
      </div>
    </section>

  </main><!-- End #main -->
 
</template>

<script>
import axios from "axios";

export default {
  props: ["item"],

  data() {
    return {
      error: {},
      success: false,
      compartilhamentos: {},
      toRemove: {},
      check: false,
      form: {},
      formAberto: false,
      statusForm: [],

      httpOptions: {
          baseURL: this.$root.config.url,
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + this.$root.credentials.token
          }
      }
    };
  },

  created: function () {
    this.getCompartilhamentos();
    this.form = {emailUsuario: '', idItem: this.item.id, dataInicio: '', dataTermino: ''};
  },

  methods: {
    getCompartilhamentos: function () {
      axios
        .get(`/api/compartilhamento/?idItem=${this.item.id}`, this.httpOptions)
        .then(response => {
          this.compartilhamentos = response.data.data;
        })
    },

    goBackToList: function () {
      this.$router.replace("/item/list");
    },

    remove: function(compartilhamento) {
      this.check = false;

      axios
        .post(`/api/compartilhamento/${compartilhamento.id}/status/`, {status:"CANCELADO"}, this.httpOptions)
        .then(response => {
          compartilhamento.status = response.data.data.status;
        })
        .catch((error) => {
          this.error[compartilhamento.id] = error.response.data.errors;
        });
    },

    confirma: function(compartilhamento) {
      this.toRemove = compartilhamento
      this.check = true;
    },

    abrirForm: function() {
      this.statusForm = [];
      this.formAberto = true;
    },

    cadastrar: function() {
      this.formAberto = false;

      if (this.form.emailUsuario == '') {
        this.statusForm[0] = "Email não foi preenchido."
        return
      } else if (this.form.dataInicio == '') {
        this.statusForm[0] = "Data início não foi escolhida."
        return
      } else if (this.form.dataTermino == '') {
        this.statusForm[0] = "Data término não foi escolhida."
        return
      }

      axios
        .post(`/api/compartilhamento/`, this.form, this.httpOptions)
        .then(response => {
          this.statusForm[0] = 'Compartilhamento registrado com sucesso!';
          this.getCompartilhamentos();
        })
        .catch((error) => {
          const errors = error.response.data.errors;

          for (let key of Object.keys(errors)) {
            this.statusForm.push(errors[key]);
          }
        });
    }
  },

  filters: {
    readableDate(date){
      return new Date(date).toLocaleDateString('pt-BR', {
        timeZone:"UTC"
      });
    }
  }
};
</script>

<style lang="css" scoped>
div.form-items-compartilhados {
  margin-top: 32px;
}
div.success {
  border: 1px solid green;
  background: lightgreen;
  padding: 8px;
  margin-bottom: 24px;
}
</style>