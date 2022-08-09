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
          <div class="token-enviado row">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Token enviado!</h2>
            <h6 class="form-subtitle mx-3">Um token para recuperação de senha foi enviado para o seu e-mail. Clique no link deste e-mail para entrar com uma nova senha.</h6>
            
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
div.token-enviado {
  margin-top: 32px;
}
div.link-login {
  margin-top: 32px;
}
</style>