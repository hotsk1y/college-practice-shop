<template>
  <div class="products">
    <form class="searchbar">
      <input placeholder="Пошук" v-model="search" />
      <input type="submit" class="btn" />
      <div v-if="cart.length">
        <button @click="toggleCart"><b>{{isOpen ? 'Close cart' : 'Open cart'}}</b></button>
      </div>
    </form>
    <div class="product" v-for="item in filteredItems" v-bind:key="item.id">
      <div class="product-image">
        <img v-bind:src="item.src" />
      </div>
      <div>
        <h4 class="product-title">
          <router-link v-bind:to="'/product/' + item.id">
            {{ item.item }}
          </router-link>
        </h4>
        <label>{{ item.price }}</label>
        <button class="btn" @click="addToCart(item)">Add to cart</button>
      </div>
    </div>
    <template v-if="isOpen">
      <Cart :products="cart" />
    </template>
  </div>
</template>
<script>
import products from "../data/products.js";
import Cart from "./Cart.vue";

export default {
  components: {
    Cart,
  },

  data () {
    return {
      items: [],
      search: "",
      searchResult: [],
      cart: [],
      isOpen: false,
    };
  },

  mounted () {
    this.items = products;

    this.cart = this.getCart;
  },

  methods: {
    addToCart (product) {
      this.$store.commit("addToCart", product);
    },

    toggleCart () {
      this.isOpen = this.isOpen ? false : true;
    },
  },
  computed: {
    filteredItems () {
      if (!this.search) {
        return this.items;
      }
      return this.items.filter((element) => {
        return element.item.toUpperCase().includes(this.search.toUpperCase());
      });
    },

    getCart () {
      return this.$store.getters.getCart;
    },
  },
};
</script>