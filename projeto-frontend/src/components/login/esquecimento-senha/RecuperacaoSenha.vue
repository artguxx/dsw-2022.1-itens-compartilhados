<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li>Recuperar Minha Senha</li>
        </ol>
        <h2>Recuperar Minha Senha</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="reinicializacao-senha row" v-if="!this.$root.credentials">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Reinicialização de senha</h2>
            <h6 class="form-subtitle mx-3">Entre com a nova senha no formulário abaixo.</h6>
            
            <form @submit.prevent="processForm">
              <div class="form-group">
                <label for="password">Nova senha</label>
                <input type="password" class="form-control" id="password" placeholder="Entre com uma senha" v-model="form.senha"></input>
                <span class="error" v-if="error.senha">{{error.senha}}</span>
              </div>

              <div class="form-group">
                <label for="password-repeat">Repita a nova senha</label>
                <input type="password" class="form-control" id="password-repeat" placeholder="Repita a sua senha" v-model="form.senhaRepetida"></input>
                <span class="error" v-if="error.senhaRepetida">{{error.senhaRepetida}}</span>
              </div>

              <button type="submit" class="btn btn-primary" style="background-color: #4154f1;">Recuperar senha</button>
            </form>

            <div class="link-login">
              <router-link class="link" :to="{ name: 'login' }">
                Lembrei da minha senha e não quero mais trocar
              </router-link>
            </div>
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
        form: { token: this.$route.query.token, email: this.$route.query.email, senha: "", senhaRepetida: "" },
        error: { }
      }
    },

    methods: {
      processForm: function() {
        axios.post(this.$root.config.url + "/api/usuario/reset", this.form)
          .then(response => {
            this.$router.replace('reseted');
            this.error = {};
          })
          .catch(error => {
            this.error = error.response.data.errors;
          });
      }
    }
  }
</script>

<style lang="css" scoped>
div.reinicializacao-senha {
  margin-top: 32px;
}
div.link-login {
  margin-top: 32px;
}
</style>