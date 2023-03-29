<template>
<div id="app">
  <HeaderComponent ref="headerComponentRef"></HeaderComponent>
  <ProductsList @addProduct="addProduct"></ProductsList>
</div>
</template>

<script>
  import HeaderComponent from "./components/HeaderComponent.vue";
  import ProductsList from "./components/ProductsList.vue";

  export default {
    name: "App",
    emits: ["addProduct"],
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
    },
    mounted() {
      this.formFilter = this.formFilterProps;
    }
  }
</script>

<style scoped>

</style>
