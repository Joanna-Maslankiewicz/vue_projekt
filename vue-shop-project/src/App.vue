<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div :key="product.id" class="col-md-6" v-for="product in products">
            <product :isInCart="isInCart(product)" @add-to-cart="addToCart" :product="product"></product>
          </div>
        </div>
      </div>
      <div class="col-md-5 my-5">
        <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :cartItems="cartItems"></cart>
      </div>
    </div>
  </div>
</template>

<script>
import products from '@/products.json';
import Cart from '@/components/Cart.vue';
import Product from '@/components/Product.vue';

export default {
  name: 'App',
  components: {
    Product,
    Cart
  },
  data() {
    return {
      products,
      cartItems: []
    }
  },
  methods: {
    addToCart({ product, quantity }) {
      const existingItemIndex = this.cartItems.findIndex((cartItem) => cartItem.product.id === product.id);

      if (existingItemIndex !== -1) {
        this.cartItems[existingItemIndex].quantity += quantity;
      } else {
        this.cartItems.push({ product, quantity });
      }
    },
    isInCart(product) {
      return this.cartItems.some((cartItem) => cartItem.product.id === product.id)
    },
    removeFromCart(product) {
      // Usuń produkt z koszyka
      const index = this.cartItems.findIndex((cartItem) => cartItem.product.id === product.id);

      if (index !== -1) {
        this.cartItems.splice(index, 1);
      }
    },
    pay() {
      this.cart = []
      alert('Shopping completed!')
    }
  }
}
</script>

<style scoped>
  body {
    background-color: antiquewhite;
  }
</style>