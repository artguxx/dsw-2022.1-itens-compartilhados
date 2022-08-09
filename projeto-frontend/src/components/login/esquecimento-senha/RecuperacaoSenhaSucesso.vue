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
          <div class="senha-reinicializada row">
          <div class="col-md-4 col-md-offset-4 text-left">
            <h2 class="form-title">Senha trocada!</h2>
            <h6 class="form-subtitle mx-3">A sua senha foi trocada. Você pode utilizar esta nova senha para acessar o sistema.</h6>
            
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
div.senha-reinicializada {
  margin-top: 32px;
}
div.link-login {
  margin-top: 32px;
}
</style>