<template>
  <div class="home">
    <section class="hero is-medium mb-6">
      <div class="surat">
        <div class="hero-body has-text-centered">
          <p class="title mb-6">

          </p>
          <p class="subtitle">

          </p>
        </div>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">LATEST PRODUCTS</h2>
      </div>

      <ProductBox
          v-for="product in latestProducts"
          v-bind:key="product.id"
          v-bind:product="product" />
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

    document.title = 'Home | YNAMLY SHOP'
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading', true)

      await axios
          .get('/api/v1/latest-products/')
          .then(response => {
            this.latestProducts = response.data
          })
          .catch(error => {
            console.log(error)
          })
      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>

<style scoped>
.surat {
  background-repeat: unset;
  background-size: cover;
  background-image: url('../assets/ynamly.png');
  width: 100%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  height: auto;
}
</style>

