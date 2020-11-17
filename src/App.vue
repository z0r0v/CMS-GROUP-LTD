<template>
    <div id="app">
        <List :content="data.products" :inCart="inCart"></List>
        <InCartComponent :inCart="inCart"></InCartComponent>
    </div>
</template>

<script>
    import List from "./components/List";
    import * as data from './assets/data.js';
    import InCartComponent from "./components/InCartComponent";
    export default {
        name: 'App',
        components: {
            List,
            InCartComponent
        },
        data() {
            return {
                data,
                inCart: [],
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
