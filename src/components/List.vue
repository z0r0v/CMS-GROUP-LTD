<template>
    <div class="product-list">
        <div class="product-list__item" v-for="(item, index) in content" :key="index">
            <ProductCart
                    :data="item"
                    :inCart="inCart"
                    :addToCart = "addToCart"
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
        methods: {
            addToCart: function (id) {
                const product = this.content.find(item => item.id === id);
                if (!this.inCart.includes(product)) {
                    this.inCart.push(product);
                }
            }
        }
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