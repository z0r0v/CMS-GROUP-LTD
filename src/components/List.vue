<template>
    <div>
        <span v-on:click="getData">getData</span>
    </div>
</template>

<script>
    export default {
        name: "List",
        methods: {
            getData: function () {
                console.log(this.data);
            }
        }
    }
</script>

<style scoped>

</style>