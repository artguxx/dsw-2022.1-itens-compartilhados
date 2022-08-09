<template lang="html">
  <main id="main">

    <!-- ======= Breadcrumbs ======= -->
    <section class="breadcrumbs">
      <div class="container">

        <ol>
          <li><a href="/">Home</a></li>
          <li>Trocar Senha</li>
        </ol>
        <h2>Trocar Senha</h2>

      </div>
    </section><!-- End Breadcrumbs -->

    <section class="inner-page">
      <div class="container">
        <div class="senha-trocada row">
          <div class="col-md-10 col-md-offset-1 text-left">
            <h2 class="form-title">Senha trocada!</h2>
            <h6 class="form-subtitle mx-3">A sua senha foi trocada. Você deve utilizar esta nova senha para acessar o sistema nas próximas vezes.</h6>
            
            <div class="link-home">
              <router-link class="link" :to="{ name: 'home' }">
                Ir para a homepage.
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
div.senha-trocada {
  margin-top: 32px;
}
div.link-home {
  margin-top: 32px;
}
</style>