<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li><router-link class="link" :to="{ name: 'item-list' }">Itens Compartilhados</router-link></li>
          <li>Novo Item</li>
        </ol>
        <h2>Novo Item</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="form-items-compartilhados row" v-if="this.$root.credentials">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Novo item compartilhado</h2>
            <h6 class="form-subtitle mx-3">Entre com os dados do novo item compartilhado.</h6>

            <div class="success" v-if="success">
              Os dados do item foram salvos.
            </div>

            <form @submit.prevent="processForm">
              <div class="form-group">
                <label for="nome">Nome</label>
                <input type="text" class="form-control" id="nome" placeholder="Entre o nome do item" v-model="item.nome">
                <span class="error" v-if="error.nome">{{error.nome}}</span>
              </div>

              <div class="form-group">
                <label for="descricao">Descrição</label>
                <textarea rows="3" cols="80" class="form-control" id="descricao" placeholder="Descreva o item" v-model="item.descricao"/>
                <span class="error" v-if="error.descricao">{{error.descricao}}</span>
              </div>

              <div class="form-group">
                <label for="tipo">Tipo</label>
                <select class="form-control" id="tipo" v-model="item.tipo">
                  <option value="">Selecione o tipo do item</option>
                  <option value="UNICO">Item único</option>
                  <option value="MULTIPLO">Item múltiplo</option>
                </select>
                <span class="error" v-if="error.tipo">{{error.tipo}}</span>
              </div>

              <button type="submit" class="btn btn-primary" style="background-color: #4154f1">Enviar</button>
            </form>
          </div>
        </div>
      </div>
    </section>

  </main><!-- End #main -->
  
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      item: { nome: "", descricao: "", tipo: "" },

      error: {},

      success: false,

      httpOptions: {
          baseURL: this.$root.config.url,
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + this.$root.credentials.token
          }
      },
    }
  },

  methods: {
    processForm: function() {
      axios.put("/api/item/novo", this.item, this.httpOptions)
        .then(response => {
          this.success = true;
          this.error = {};
          setTimeout(this.goBackToList, 3000);
        })
        .catch(error => {
          this.error = error.response.data.errors;
        });
    },

    goBackToList: function() {
      this.$router.replace('/item/list');
    }
  }
}
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