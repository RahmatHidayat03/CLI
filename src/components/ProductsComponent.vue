<template>
  <div>
    <h1>IDShop</h1>
    <navbar-component
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle-slide="ToggleSlider"
      @delete-item="deleteItem"
    ></navbar-component>
    <price-slider
      :sliderStatus="sliderStatus"
      :maximum.sync="maximum"
    ></price-slider>
    <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente laborum
      nihil atque, aut cum vitae, iste iusto accusamus aliquid obcaecati nemo,
      temporibus nostrum magnam aperiam accusantium nesciunt dolorum dicta nisi!
    </p>
    <product-list
      :products="products"
      :maximum="maximum"
      @add-item="addItem"
    ></product-list>
  </div>
</template>

<script>
import NavbarComponent from "./NavbarComponent.vue";
import PriceSlider from "./PriceSlider.vue";
import ProductList from "./ProductList.vue";

export default {
    name: "products",
    props: [
        "products",
        "maximum",
        "cart",
        "cartQty",
        "cartTotal",
        "sliderStatus",
        "sliderState"
    ],
    components: {
        NavbarComponent,
        PriceSlider,
        ProductList,
    },
    methods: {
        ToggleSlider() {
            this.$emit('toggle');
        },
        addItem(item) {
            this.$emit('add', item)
        },
        deleteItem(index) {
            this.$emit('delete', index)
        }
    }
}
</script>
