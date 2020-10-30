<template>
    <div id="app">
        <span v-on:click="getData">123</span>
        <List v-bind:content="data"></List>
    </div>
</template>

<script>
    import List from "./components/List";
    import * as data from './assets/data.js';
    export default {
        name: 'App',
        components: {
            List,
        },
        data() {
            return {
                data,
            }
        },
        methods: {
            getData: function () {
                console.log(this.data.products);
            }

        },
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
