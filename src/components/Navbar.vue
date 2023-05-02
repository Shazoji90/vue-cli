<template>
  <nav class="navbar bg-white fixed-top py-0 px-2">
    <div class="navbar-text ms-auto d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slide')"
      >
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ms-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge rounded-pill bg-success">{{ cartQty }}</span>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-end"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span
                class="badge rounded-pill bg-warning text-dark align-text-top me-1"
              >
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ (item.product.price * item.qty) | currencyFormat }}</b>
              <a
                href="#"
                class="badge text-bg-danger text-decoration-none"
                @click.stop="$emit('delete-item', index)"
                >-</a
              >
            </div>
          </div>
          <router-link
            class="btn btn-sm btn-outline-info text-dark float-end me-2"
            to="/checkout"
            >Checkout</router-link
          >
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";
export default {
  name: "navbar",
  components: {
    FontAwesomeIcon,
    Price,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
