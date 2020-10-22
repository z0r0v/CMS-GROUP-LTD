<template>
    <div id="app">
        <ProductComponent></ProductComponent>
    </div>
</template>

<script>

import ProductComponent from './components/ProductComponent.vue'
export default {
  name: 'App',
  components: {
      ProductComponent,
  },
}
</script>

<style>
#app {
    display: flex;
    flex-wrap: wrap;
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
