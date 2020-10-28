<template>
  <div id="app">
      123
  </div>
</template>

<script>
    // import products from "src/assets/data.js";
    import dataJS from "src/assets/data.json";


export default {

  name: 'App',
  components: {
  },
    data() {
        return {
            dataJS,
        }
    },
    methods: {
      returnData: function () {
            // console.log(this.products)
          // console.log(this.dataJS);
      }
    }
}



</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
