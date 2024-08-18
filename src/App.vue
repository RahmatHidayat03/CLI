<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente laborum
      nihil atque, aut cum vitae, iste iusto accusamus aliquid obcaecati nemo,
      temporibus nostrum magnam aperiam accusantium nesciunt dolorum dicta nisi!
    </p>
    <product-list
      v-if="products.length > 0"
      :products="products"
      :maximum="50"
    ></product-list>
    <p v-else>Loading products...</p>
    <!-- <Product-list :product="products" :maximum="maximum"></Product-list> -->
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function () {
    return {
      maximum: 50,
      products: [],
    };
  },
  components: {
    ProductList,
  },
  mounted() {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>
