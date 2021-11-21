<template>
  <div class="cart">
    <h1>Cart</h1>
    <div class="cart-item" :key="index" v-for="(item, index) in products">
      <b>{{ index + 1 }}.</b>
      <span>{{ item.item }}</span>
      <span>({{ item.price }})</span>
    </div>
      <b>Total Price: ${{ getTotalPrice(products).toFixed(1) }}</b>
  </div>
</template>

<script>
export default {
  props: {
    products: null,
  },
  methods: {
    getTotalPrice: function (products) {
      return products.reduce((acc, item) => acc + item.price, 0);
    },
  },
};
</script>

<style scoped>
.cart {
  width: 500px;
  margin: 20px;
  padding: 10px;
  border: 1px solid #000;
}

.cart-item {
  margin-bottom: 15px;
}
</style>