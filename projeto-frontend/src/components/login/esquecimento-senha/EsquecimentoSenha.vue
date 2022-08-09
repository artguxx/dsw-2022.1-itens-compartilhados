<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li>Esqueci Minha Senha</li>
        </ol>
        <h2>Esqueci Minha Senha</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="recuperacao-senha row" v-if="!this.$root.credentials">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Recuperar senha</h2>
            <h6 class="form-subtitle mx-3">Entre com o seu e-mail no formulário abaixo. Um link para troca de senha será enviado por e-mail.</h6>

            <form  @submit.prevent="processForm">
              <div class="form-group">
                <label for="email">E-mail</label>
                <input type="text" class="form-control" id="email" placeholder="Entre o seu e-mail" v-model="form.email">
                <span class="error" v-if="error.email">{{error.email}}</span>
              </div>

              <button type="submit" class="btn btn-primary" style="background-color: #4154f1;">Recuperar</button>
            </form>

            <div class="link-login">
              <router-link class="link" :to="{ name: 'login' }">
                Lembrou sua senha?
              </router-link>
            </div>
            
            <div class="link-criar-conta">
              <router-link class="link" :to="{ name: 'create-account' }">
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
        form: { email: "" },
        error: { }
      }
    },

    methods: {
      processForm: function() {
        axios.post(this.$root.config.url + "/api/usuario/esqueci", this.form)
          .then(response => {
            this.$router.replace('token-sent');
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
div.recuperacao-senha {
  margin-top: 32px;
}
div.link-login {
  margin-top: 32px;
}
div.link-criar-conta {
  margin-top: 8px;
}
</style>