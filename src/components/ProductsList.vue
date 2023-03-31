<template>
 <main>
      <div class="products">
          <div class="product-item" v-for="product in filteredProducts" :key="product.id_product">
              <img :src="imgCatalog" alt="Some img">
              <div class="desc">
                  <h3>{{product.product_name}}</h3>
                  <p>{{product.price}} $</p>
                  <button class="buy-btn" @click='addProduct(product)'>Купить</button>
                  
              </div>
          </div>
      </div>
  </main>
</template>
  
<script>
  const API = 'http://localhost:3000';

  export default {
    name: "ProductsList",
    emits: ["addProduct"],
    data() {
      return {
        search: "",
        catalogUrl: `/api/products`,
        cartUrl: `/api/cart`,
        imgCatalog: "https://placehold.it/200x150",
        products: [],
        cart: [],

      }
    },

    methods: {
      
      getJson(url){
        return fetch(url)
          .then(result => result.json())
          .catch(error => {
            console.log(error);
          })
      },

      addProduct(product){
        this.$emit("addProduct", product);
      },

      handleSearch(search){
        this.search = search;
      }
    },

    computed: {
      filteredProducts() {
        if (this.search !== "") {
          const regexp = new RegExp(this.search, 'i');
          this.filtered = this.products.filter(product => regexp.test(product.product_name));
          return this.filtered;
        }
        return this.products;
      },
    },

    mounted(){
      this.getJson(`${API + this.catalogUrl}`)
        .then(data => {
            this.products = [...data];
        })

      this.getJson(`${API + this.cartUrl}`)
      .then(data => {
          this.cart = data.contents;
      })
    }
  }
</script>

<style scoped>

</style>
