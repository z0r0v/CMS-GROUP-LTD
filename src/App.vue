<template>
    <div id="app">
        <ProductComponent></ProductComponent>
        <CartComponent></CartComponent>
    </div>
</template>

<script>

import ProductComponent from './components/ProductComponent.vue'
import CartComponent from "./components/CartComponent";

export default {
  name: 'App',
  components: {
      ProductComponent,
      CartComponent
  }
}
</script>

<style>
#app {
    display: flex;
    width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
    .no-display {
        display: none;
    }
</style>
