<template>
<div id="app">
  <HeaderComponent></HeaderComponent>
  <!-- <main>
      <div class="products">
          <div class="product-item" v-for="product in filteredProducts" :key="product.id_product">
              <img :src="imgCatalog" alt="Some img">
              <div class="desc">
                  <h3>{{product.product_name}}</h3>
                  <p>{{product.price}} $</p>
                  <button class="buy-btn" @click="addProduct(product)">Купить</button>
              </div>
          </div>
      </div>
  </main> -->
</div>
</template>

<script>
  import HeaderComponent from "./components/HeaderComponent.vue"

  export default {
    name: "App",
    components: { HeaderComponent },
    data() {
      return {
        formFilter: {},
      }
    },
    props: {
      awbs: {
        type: Object,
      },
      formFilterProps: {
        type: Object,
      }
    },
    methods: {
      setFilter() {
        this.$emit('setFilter', this.formFilter);
      },
      resetFilter() {
        this.formFilter.reset();
      },
    },
    mounted() {
      this.formFilter = this.formFilterProps;
    }
  }
</script>

<style scoped>

</style>
