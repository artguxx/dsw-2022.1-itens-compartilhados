<template>
  <div id="app">
      <!-- ======= Header ======= -->
    <header id="header" class="header fixed-top text-bg-light">
      <div class="container-fluid container-xl d-flex align-items-center justify-content-between">

        <a href="/" class="logo d-flex align-items-center">
          <span>Shared4U</span>
        </a>

        <nav id="navbar" class="navbar">
          <ul>
            <li><a class="nav-link scrollto" href="/">Home</a></li>
            <li v-if="$root.credentials"><router-link class="link" :to="{ name: 'item-list' }">Itens Compartilhados</router-link></li>
            <li v-if="$root.credentials"><router-link class="link" :to="{ name: 'item-recebido' }">Itens Recebidos</router-link></li>
            <li class="dropdown"  v-if="$root.credentials"><a class="getstarted scrollto"><span class="text-white">Olá, {{$root.credentials.nome}}</span></a>
              <ul>            
                <li><router-link :to="{ name: 'change-password' }">Trocar senha</router-link></li>
                <li><a @click="logout" style="cursor: pointer;">Logout</a></li>
              </ul>
            </li>
            <li v-else><router-link class="getstarted scrollto" :to="{ name: 'login' }">Login</router-link></li>
          </ul>
          <i class="bi bi-list mobile-nav-toggle"></i>
        </nav><!-- .navbar -->
      </div>
    </header><!-- End Header -->

      <router-view></router-view>
   
    <!-- ======= Footer ======= -->
    <footer id="footer" class="footer">
      <div class="footer-top">
        <div class="container">
          <div class="row gy-4">
            <div class="col-lg-6 col-md-12 footer-info">
              <a href="/" class="logo d-flex align-items-center">
                <span>Shared4U</span>
              </a>
              <p>Shared4U eh uma plataforma onde voce pode compartilhar seus itens com outros usuarios gratis!
              Venha participar da nossa comunidade e desfrute dessa experiencia unica que proporcionamos!
              Crie sua conta agora mesmo e comece a compartilhar!!</p>
            </div>

            <div class="col-lg-5 col-md-12 footer-contact text-center text-md-start">
              <h4>Fale Conosco</h4>
              <p>
                Av. Pasteur 458 <br>
                Rio de Janeiro, RJ 22290-255<br>
                Brasil <br><br>
                <strong>Telefone:</strong> +55 (21) 3223-8020<br>
                <strong>Email:</strong> bsi.coordenacao@uniriotec.br <br>
              </p>

            </div>

          </div>
        </div>
      </div>

      <div class="container">
        <div class="copyright">
          &copy; Copyright <strong><span>Arthur e Lucas</span></strong>. All Rights Reserved
        </div>
        <div class="credits">
          Designed by Arthur & Lucas
        </div>
      </div>
    </footer><!-- End Footer -->
  </div>
</template>

<script>
  export default {
    data () {
      return { }
    },

    methods: {
      logout: function() {
        this.$root.credentials = null;
        this.$router.go('home');
      }
    }
  }
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  margin-top: 30px;
}
.modal-content-credentials {
    display: flex;
    flex-direction: column;
    padding: 12px;
}
.button-modal {
  border: none;
  outline: none;
  background: none;
}
span.greetings {
  color: white;
  margin: 0 4px;
}
li {
  margin: 0 4px;
}
li.login-commands {
  color: white;
  padding-top: 15px;
  margin-right: 32px;
}
li.login-commands a {
  display: inline;
  padding: 15px 8px;
}
li.user-commands {
  color: white;
  padding-top: 15px;
  margin-right: 32px;
}
li.user-commands span.greetings {
  margin-right: 12px;
}
li.user-commands a {
  display: inline;
  padding: 15px 8px;
}
.site-footer
{
  background-color:#26272b;
  padding:45px 0 20px;
  font-size:15px;
  line-height:24px;
  color:#737373;
  margin-top: 200px !important;
}
.site-footer hr
{
  border-top-color:#bbb;
  opacity:0.5
}
.site-footer hr.small
{
  margin:20px 0
}
.site-footer h6
{
  color:#fff;
  font-size:16px;
  text-transform:uppercase;
  margin-top:5px;
  letter-spacing:2px
}
.site-footer a
{
  color: white;
}
.site-footer a:hover
{
  color: white;
  text-decoration:none;
}
.footer-links
{
  padding-left:0;
  list-style:none
}
.footer-links li
{
  display:block
}
.footer-links a
{
  color:#737373
}
.footer-links a:active,.footer-links a:focus,.footer-links a:hover
{
  color: white;
  text-decoration:none;
}
.footer-links.inline li
{
  display:inline-block
}
.site-footer .social-icons
{
  text-align:right
}
.copyright-text
{
  margin:0
}
@media (max-width:991px)
{
  .site-footer [class^=col-]
  {
    margin-bottom:30px
  }
}
@media (max-width:767px)
{
  .site-footer
  {
    padding-bottom:0
  }
  .site-footer .copyright-text,.site-footer .social-icons
  {
    text-align:center
  }
}
@media (max-width:767px)
{
  .social-icons li.title
  {
    display:block;
    margin-right:0;
    font-weight:600
  }
}
</style>
