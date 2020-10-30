<template>
    <div class="product-cart">
        <h3>{{name}}</h3>
        <p>{{description}}</p>
        <p>{{cost}}</p>
    </div>
</template>
<script>
    export default {
        name: "ProductCart",
        props: [
            "name",
            "description",
            "cost",
        ],
    }
</script>

<style lang="scss">
    .product-cart {
        border: 1px solid black;
    }
</style>