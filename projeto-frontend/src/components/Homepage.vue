<template lang="html">
  <div>
    <!-- <div class="jumbotron text-center">
      <div v-if="$root.credentials">
        <div v-if="this.qtdItensAbertos > 0">
          <vue-typed-js :strings="[`Você tem ${this.qtdItensAbertos} ite${this.qtdItensAbertos == 1 ? 'm':'ns'} recebidos abertos.`]" :loop="true" :showCursor="false" class="d-flex justify-content-around">
            <p class="typing text-danger"></p>
          </vue-typed-js>
        </div>
        <div v-else>
          <vue-typed-js :strings="['Você não tem itens recebidos abertos.']" :loop="true" :showCursor="false" class="d-flex justify-content-around">
            <p class="typing text-primary"></p>
          </vue-typed-js>
        </div>
        
      </div>
      <div v-else>
        <vue-typed-js :strings="['Faca login para ter a experiencia completa!']" :loop="true" :showCursor="false" class="d-flex justify-content-around">
            <p class="typing text-danger"></p>
          </vue-typed-js>
      </div>
    </div> -->

<!-- ======= Hero Section ======= -->
  <section id="hero" class="hero d-flex align-items-center">

    <div class="container">
      <div class="row">
        <div class="col-lg-6 d-flex flex-column justify-content-center">
          <vue-typed-js :strings="['Nós oferecemos um sistema de compartilhamento moderno!']" :loop="false" :showCursor="false" class="d-flex justify-content-around">
            <h1 class="typing" data-aos="fade-up"></h1>
          </vue-typed-js>
          <div data-aos="fade-up" data-aos-delay="600">
            <div class="text-center text-lg-start">
            </div>
          </div>
        </div>
        <div class="col-lg-6 hero-img" data-aos="zoom-out" data-aos-delay="200">
          <img src="/src/assets/img/hero-img.png" class="img-fluid" alt="">
        </div>
      </div>
    </div>

  </section><!-- End Hero -->

  <!-- ======= Values Section ======= -->
    <section id="values" class="values">

      <div class="container" data-aos="fade-up">

        <header class="section-header">
          <h2>Nossos valores</h2>
          <p>Alguns dos nossos valores</p>
        </header>

        <div class="row">

          <div class="col-lg-4" data-aos="fade-up" data-aos-delay="200">
            <div class="box">
              <img src="/src/assets/img/values-1.png" class="img-fluid" alt="">
              <h3>Senso de comunidade</h3>
              <p>Faça parte de uma comunidade incrível, onde você pode interagir e fazer amizades.</p>
            </div>
          </div>

          <div class="col-lg-4 mt-4 mt-lg-0" data-aos="fade-up" data-aos-delay="400">
            <div class="box">
              <img src="/src/assets/img/values-2.png" class="img-fluid" alt="">
              <h3>Inovação</h3>
              <p>Compartilhe qualquer tipo de item, sendo eles únicos ou múltiplos.</p>
            </div>
          </div>

          <div class="col-lg-4 mt-4 mt-lg-0" data-aos="fade-up" data-aos-delay="600">
            <div class="box">
              <img src="/src/assets/img/values-3.png" class="img-fluid" alt="">
              <h3>Flexibilidade</h3>
              <p>Cancele seus compartilhamentos a hora que achar mais conveniente com segurança garantida.</p>
            </div>
          </div>

        </div>

      </div>

    </section><!-- End Values Section -->

 <!-- ======= Features Section ======= -->
    <section id="features" class="features">

      <div class="container" data-aos="fade-up">

        <header class="section-header">
          <h2>Características</h2>
          <p>Algumas de nossas características</p>
        </header>

        <div class="row">

          <div class="col-lg-6">
            <img src="/src/assets/img/features.png" class="img-fluid" alt="">
          </div>

          <div class="col-lg-6 mt-5 mt-lg-0 d-flex">
            <div class="row align-self-center gy-4">

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="200">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Segurança</h3>
                </div>
              </div>

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="300">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Facilidade</h3>
                </div>
              </div>

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="400">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Flexibilidade</h3>
                </div>
              </div>

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="500">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Inovação</h3>
                </div>
              </div>

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="600">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Comunidade</h3>
                </div>
              </div>

              <div class="col-md-6" data-aos="zoom-out" data-aos-delay="700">
                <div class="feature-box d-flex align-items-center">
                  <i class="bi bi-check"></i>
                  <h3>Inclusão</h3>
                </div>
              </div>

            </div>
          </div>

        </div> <!-- / row -->
        </div>

    </section><!-- End Features Section -->




  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        qtdItensAbertos: 0,

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

    created: function() {
      axios.get(`/api/compartilhamento/?idUsuario=${this.$root.credentials.id}`,this.httpOptions)
        .then(response => {
          this.qtdItensAbertos = response.data.data.filter(item => item.status == "ABERTO").length;
          console.log("===================================");
          console.log(this.qtdItensAbertos);
        })
        .catch(error => {
          this.error = error.response.data.errors;
        });
    }
  }
</script>

<style lang="css" scoped>
div.jumbotron {
  margin-top: 32px;
}
</style>
