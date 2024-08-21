<template>
  <div id="app" class="container mt-5">
    <checkout-component 
      :cart="cart"
      :cartTotal="cartTotal"
      @add="addItem"
      @delete="deleteItem"></checkout-component>
    <products-component
      :cart="cart"
      :cart-qty="cartQty"
      :cart-total="cartTotal"
      :maximum.sync="maximum"
      :products="products"
      :slider-status="sliderStatus"
      @toggle="ToggleSliderStatus"
      @add="addItem"
      @delete="deleteItem"></products-component>
  </div>
</template>

<script>
import checkoutComponent from './components/checkoutComponent.vue';
import ProductsComponent from './components/ProductsComponent.vue';

export default {
  name: "app",
  data() {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderStatus: false,
    };
  },
  components: {
    checkoutComponent,
    ProductsComponent
  },
  mounted() {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  computed: {
    cartTotal: function () {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    },
  },
  methods: {
    ToggleSliderStatus() {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function (product) {
      let productIndex;
      let productExist = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          productIndex = index;
          return true;
        } else {
          return false;
        }
      });

      if (productExist.length) {
        this.cart[productIndex].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
    deleteItem: function (id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },
  },
};
</script>
