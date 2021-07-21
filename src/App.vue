<template>
  <div id="wrapper"  class="has-background-black">
    <nav class="navbar is-black">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item"><img src="./assets/logoBranco.png" alt=""></router-link>

        <a class="navbar-burger has-background-black has-text-white" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>
      
      <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu }">
        <div class="navbar-start has-background-black">
          <div class="navbar-item">
            <form method="get" action="/search">
              <div class="field has-addons">
                <div class="control">
                  <input type="text" class="input" placeholder="What are you looking for?" name="query">
                </div>
                <div class="control">
                  <button class="button is-success">
                    <span class="icon">
                      <i class="fas fa-search"></i>
                    </span>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
        <div class="navbar-end has-background-black">
          <router-link to="/aliancas" class="navbar-item has-text-white">Alianças</router-link>
          <router-link to="/biochip" class="navbar-item has-text-white">Biochips</router-link>
          <router-link to="/cucuias" class="navbar-item has-text-white">Cucuias</router-link>
          <router-link to="/arcos" class="navbar-item has-text-white">Arcos</router-link>
          <router-link to="/signos" class="navbar-item has-text-white">Signos</router-link>
          <router-link to="/about" class="navbar-item has-text-white">About Us</router-link>
        
          <div class="navbar-item">
            <div class="buttons">
              <template v-if="$store.state.isAuthenticated">
                <router-link to="/my-account" class="button is-info is-focused">My account</router-link>
              </template>

              <template v-else>
                <router-link to="/log-in" class="button is-info is-focused">Log in</router-link>
              </template>

              <router-link to="/cart" class="button is-success is-focused">
                <span class="icon"><i class="fas fa-shopping-cart"></i></span>
                <span>Cart ({{ cartTotalLength }})</span>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="section has-background-dark">
      <router-view/>
    </section>
    
    <footer class="footer has-background-black">
      <div class="has-text-centered has-text-black">
        <a href="https://www.facebook.com/TribusDmart" target="_blank" class="button is-medium is-facebook">
          <span class="icon">
            <i class="fab fa-facebook"></i>
          </span>
        </a>
         | 
        <a href="https://www.instagram.com/tribus_dmart" target="_blank" class="button is-medium is-instagram">
          <span class="icon">
            <i class="fab fa-instagram"></i>
          </span>
        </a>
      </div>
      <br>
      <p class="has-text-centered has-text-white">Copyright DMarT (c) 2021</p>
    </footer>
  </div>
</template>

<style lang="scss">
@import '../node_modules/bulma';
</style>

<script>
export default {
  data() {
    return {
      showMobileMenu: false,
    }
  }
}
</script>