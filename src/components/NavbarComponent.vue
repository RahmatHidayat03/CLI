<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$emit('toggle-slide')">
        <font-awesome-icon icon="fa-solid fa-dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <i class="fa-solid fa-cart-shopping mx-0"></i>
          <font-awesome-icon icon="cart-shopping" class="mx-2" />
          <price-component :value="Number(cartTotal)"></price-component>
        </button>
        <div
          class="dropdown-menu dropdown-menu-right"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span class="badge badge-pill badge-warning align-text-top mr-1">
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ (item.qty * item.product.price) | currencyFormat }}</b>
              <a
                href="#"
                class="badge badge-danger text-white"
                @click.stop="$emit('delete-item', index)"
                >-</a
              >
            </div>
          </div>
          <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-1" to="/checkout">Checkout</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import PriceComponent from "./PriceComponent.vue";

export default {
  name: "navbar-component",
  components: {
    FontAwesomeIcon,
    PriceComponent,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
