<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li>Login</li>
        </ol>
        <h2>Login</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="row" v-if="!$root.credentials">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Login</h2>
            <h6 class="form-subtitle mx-3">Entre com as suas credenciais para o login.</h6>

            <form @submit.prevent="processForm">
              <div class="form-group">
                <label for="username">Login</label>
                <input type="text" class="form-control" id="username" placeholder="Entre o seu login" v-model="form.email">
                <span class="error" v-if="error.all">{{error.all}}</span>
              </div>

              <div class="form-group">
                <label for="password">Senha</label>
                <input type="password" class="form-control" id="password" placeholder="Entre e sua senha" v-model="form.senha" autocomplete="on">
              </div>

              <button type="submit" class="btn btn-primary" style="background-color: #4154f1;">Logar</button>
            </form>

            <div class="link-recuperar-senha">
              <router-link class="link" :to="{ name: 'forgot-password' }" replace>
                Recuperar a minha senha
              </router-link>
            </div>
            
            <div class="link-criar-conta">
              <router-link class="link" :to="{ name: 'create-account' }" replace>
                Criar nova conta
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
        form: { email: "", senha: "" },
        error: { }
      }
    },

    methods: {
      processForm: function() {
        axios.post(this.$root.config.url + "/auth", this.form)
          .then(response => {
            this.$root.credentials = response.data.data;
            this.$router.go('home');
            this.error = {};
          })
          .catch(error => {
            this.error = error.response.data.errors;
          })
      }
    }
  }
</script>

<style lang="css" scoped>
div.login {
  margin-top: 32px;
}
div.link-recuperar-senha {
  margin-top: 32px;
}
div.link-criar-conta {
  margin-top: 8px;
}
</style>