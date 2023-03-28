<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <div id="app">
    <header>
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

      <div class="wrapper">
        <HelloWorld msg="You did it!" />
      </div>
    </header>

    <main>
      <TheWelcome />
    </main>
  </div>
</template> -->

<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button @click="showCheckout">{{this.cart.length}}Checkout</button>
      <div id="Banner">
            <button v-if="enableCart" @click="toggleShowProduct"> {{totalItemsInTheCart}}> Checkout
              <font-awesome-icon :icon="['fas', 'shopping-cart']" />
            </button>
            <button disabled v-else>View Cart
              <font-awesome-icon :icon="['fas', 'cart-arrow-down']" />
            </button>
      </div>
    </header>
    <main>
      <component :is="currentView"></component>
    </main>
  </div>
</template>
<script>
import ProductList from './components/ProductList.vue';
import Checkout from './components/Checkout.vue';

export default {
  name: "#app",
  data() {
    return {
      sitename: "Vue.js Pet Depot",
      cart: [],
      currentView: ProductList
    }
  },
  components: {
    ProductList, Checkout
  },
  methods: {
    showCheckout() {
      if (this.currentView === ProductList) {
        this.currentView = Checkout;
      } else {
        this.currentView = ProductList;
      }
    }
  },
  computed: {
    totalItemsInTheCart: function() {
      return this.cart.length || "";
    }
  }
};
</script>

<style scoped> 
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
