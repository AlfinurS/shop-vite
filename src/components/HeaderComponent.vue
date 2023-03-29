<template>
  <header>
    <div class="logo">E-shop</div>
    <div class="cart">
      <form action="#" class="search-form">
        <input 
          v-model="search"
          @input="(event) => handleSearch(event.target.value)"
          type="text"
          class="search-field"
          placeholder="Поиск товаров"
        >
        <button class="btn-search" type="submit">
          <i class="fas fa-search"></i>
        </button>
      </form>
      <button class="btn-cart" type="button" @click="showCart">Корзина</button>

      <div class="cart-block" v-if="isShowCart">
        <p v-if="cart.length === 0">Корзина пустая</p>
        <div class="cart-block-item" v-for="product in cart" :key="product.id_product">
          <img :src="imgCatalog" alt="Some img">
          <h3>{{product.product_name}}</h3>
          <p>{{product.price * product.quantity}} $</p>
          <p>{{product.quantity}} шт</p>
          <button class="delete-btn" @click="deleteProduct(product)">Удалить</button>
        </div>
      </div>

    </div>
  </header>
</template>
  
<script>
  const API = 'https://raw.githubusercontent.com/GeekBrainsTutorial/online-store-api/master/responses';

  export default {
    name: "HeaderComponent",
    emits: ["handleSearch"],
    props: {
      product: {
        type: Object,
        default: () => ({}),
      },
    },

    data() {
      return {
        search: "",
        cartUrl: `/getBasket.json`,
        imgCatalog: "https://placehold.it/200x150",
        isShowCart: false,
        cart: [],
        deleteCartUrl: `/deleteFromBasket.json`,
      }
    },

    methods: {
      showCart(){
        this.isShowCart = !this.isShowCart;
      }, 

      handleSearch(search){
        this.$emit("handleSearch", search);
      },

      getJson(url){
        return fetch(url)
          .then(result => result.json())
          .catch(error => {
            console.log(error);
          })
      },

      addProduct(product){
        const productFind = this.cart.find((item) => item.id_product === product.id_product);
        if (productFind) {
          ++productFind.quantity;
          //this.showCart(productFind)
        } else {
          const cartProduct = JSON.parse(JSON.stringify(product))
          cartProduct.quantity = 1;
          this.cart.push(cartProduct);
        }
      },

      deleteProduct(product){
        this.getJson(`${API + this.deleteCartUrl}`)
          .then(data => {
            if(data.result===1){
              const productFind = this.cart.find((item) => item.id_product === product.id_product);
              if (productFind.quantity > 1){
                productFind.quantity--;
              } else {
                this.cart.splice(this.cart.indexOf(productFind), 1);
              }
            }
          })
      },
    },


    mounted(){
      
      this.getJson(`${API + this.cartUrl}`)
        .then(data => {
            this.cart = data.contents;
        })
    }
  }
</script>

<style scoped>

</style>
