<template>
  <div id="app">
    <component :is="layout">
      <router-view/>
    </component>
  </div>
</template>

<script>
  import MainLayout from '@/layouts/MainLayout';
  import Error from '@/components/app/Error';
  import Cart from '@/components/app/Cart';
  import CartItem from '@/components/app/CartItem';
  import Filter from '@/components/app/Filter';
  import Product from '@/components/app/Product';
  import Products from '@/components/app/Products';
  import TotalSum from '@/components/app/TotalSum';
  export default {
    data: () => ({
      API: 'https://raw.githubusercontent.com/Konstantin108/Vue-store-project2/master/responses',
      userSearch: ''
    }),
    computed: {
      layout() {
        console.log()
        return (this.$route.meta.layout || 'main') + '-layout'
      }
    },
    methods: {
      getJson(url) {
        return fetch(url)
                .then(result => result.json())
                .catch(error => {
                  this.$refs.error.setError();
                })
      },
    },
    components: {
      MainLayout, Error, Cart, CartItem, Filter, Product, Products, TotalSum
    },
    mounted() {
      console.log(this);
    }
  }
</script>

<style lang="scss">
  @import 'assets/style.css';
</style>
