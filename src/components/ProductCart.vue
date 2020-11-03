<template>
    <div class="product-cart">
        <h3 v-if="data.name">{{data.name}}</h3>
        <h3 v-else>name: {{noV}}</h3>
        <p v-if="data.description">{{data.description}}</p>
        <p v-else>description: {{noV}}</p>
        <p v-if="data.cost">{{data.cost}}</p>
        <p v-else>cost: {{noV}}</p>
        <button v-on:click="handleAddToCartClick">Add to cart</button>
    </div>
</template>
<script>
    export default {
        name: "ProductCart",
        props: [
            "data",
            "inCart",
            "addToCart",
        ],
        data() {
            return {
                noV: "no value",
            }
        },
        methods: {
            handleAddToCartClick: function () {
                if(this.addToCart) {
                    this.addToCart(this.data.id);
                }
            }
        }
    }
</script>

<style lang="scss">
    .product-cart {
        border: 1px solid black;
        button {
            margin-bottom: 20px;
        }
    }
</style>

