<template>
    <div class="product-list">
        <div class="product-list__item" v-for="(item, index) in content" :key="index">
            <ProductCart
                    :data="item"
                    :inCart="inCart"
            ></ProductCart>
        </div>

    </div>
</template>
<script>
    import ProductCart from "./ProductCart";
    export default {
        name: "List",
        components: {
            ProductCart,
        },
        props: [
            "content",
            "inCart"
        ],
    }
</script>

<style lang="scss">
    .product-list {
        display: flex;
        flex-wrap: wrap;
        &__item {
            width: 25%;
        }
    }
</style>