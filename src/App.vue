<template>
<div id="app">
  <HeaderComponent ref="headerComponentRef" @handleSearch="handleSearch"></HeaderComponent>
  <ProductsList ref="productsListRef" @addProduct="addProduct"></ProductsList>
</div>
</template>

<script>
  import HeaderComponent from "./components/HeaderComponent.vue";
  import ProductsList from "./components/ProductsList.vue";

  export default {
    name: "App",
    emits: ["addProduct", "handleSearch"],
    components: { HeaderComponent, ProductsList },

    data() {
      return {
        formFilter: {},

      }
    },
/*     props: {
      awbs: {
        type: Object,
      },
      formFilterProps: {
        type: Object,
      }
    }, */
    
    methods: {
      setFilter() {
        this.$emit('setFilter', this.formFilter);
      },

      resetFilter() {
        this.formFilter.reset();
      },

      addProduct(product) {
        this.$refs.headerComponentRef.addProduct(product);
      },

      handleSearch(search) {
        this.$refs.productsListRef.handleSearch(search);
        console.log(search);
      },
    },
    mounted() {
      this.formFilter = this.formFilterProps;
    }
  }
</script>

<style scoped>

</style>
