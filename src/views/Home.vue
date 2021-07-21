<template>
<div class="home has-text-white">
    <section class="hero is-medium is-dark mb-6">
      <div class="has-text-centered">
        <p>
          <img src="./../assets/logoBranco.png" alt="Logo Dmart">
        </p>
        <p class="subtitle">
          We are one family!
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
          <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>

      <ProductBox v-for="product in latestProducts" v-bind:key="product.id" v-bind:product="product" />

    </div>

  </div>
</template>

<script>
import axios from 'axios'

import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()

    document.title = 'Home | DMarT'
  },
  methods: {
    getLatestProducts(){
      axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts = response.data
        })
        .catch(error =>{
          console.log(error)
        })
    }
  }
}
</script>
