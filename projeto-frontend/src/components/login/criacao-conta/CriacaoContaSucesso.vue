<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="index.html">Home</a></li>
          <li>Criar Conta</li>
        </ol>
        <h2>Criar Conta</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="conta-criada row">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Conta registrada!</h2>
            <h6 class="form-subtitle mx-3">Faça o login para entrar no sistema.</h6>
            
            <div class="link-login">
              <router-link class="link" :to="{ name: 'login' }">
                Ir para a página de login.
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </section>

  </main><!-- End #main -->
</template>

<script>
  export default {
  }
</script>

<style lang="css" scoped>
div.conta-criada {
  margin-top: 32px;
}
div.link-login {
  margin-top: 32px;
}
</style>