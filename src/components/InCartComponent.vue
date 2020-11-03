
<template>
<div class="in-cart">
    <h2>{{h2}}</h2>
    <div class="in-cart__items">
    <div class="item" v-for="(item, index) in inCart" :key="index">
        <ProductCart :data="item"></ProductCart>
    </div>
    </div>
</div>
</template>

<script>
    import ProductCart from "./ProductCart";
    export default {
        name: "InCartComponent",
        components: {
            ProductCart,
        },
        data(){
            return {
                h2:"Product in cart:",
            }
        },
        props: [
            "inCart",
        ],
    }
</script>

<style lang="scss">
.in-cart {
    &__items {
        display: flex;
        flex-wrap: wrap;
        .item {
            width: 25%;
        }
    }
    .product-cart {
        button {
            display: none;
        }
    }
}
</style>