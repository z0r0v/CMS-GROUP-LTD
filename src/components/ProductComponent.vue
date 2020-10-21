<template>
    <div class="product-component">
        <table v-for="(name, idx) in namesJ" :key="idx">
            <tr class="name" v-on:click="openCloseTable">
                <th colspan="2">{{name.G}}</th>
            </tr>
            <tr class="item" v-for="(nameB, idx) in name.B" :key="idx" :data-id="nameB.T">
                <td>
                    <h5>{{nameB.N}}</h5>
                    <span v-for="(good, idx) in goods" :key="idx">
                            <span v-if="good.T === nameB.T">({{good.P}})</span>
                        </span>
                </td>
                <td class="price">
                    <span v-if="nameB.T==''">{{nId}}</span>
                    <span v-else v-for="(good, idx) in goods" :key="idx">
                            <span v-if="good.T === nameB.T">{{(good.C).toFixed(2)}} {{BYN}}</span>
                      </span>
                </td>
            </tr>
        </table>
    </div>
</template>
<script>

    import dataJ from '../assets/tets/data.json';
    import namesJ from '../assets/tets/names.json';

    // console.log("goods:", dataJ.Value.Goods);
    // console.log("namesJ", namesJ);

    let goods = dataJ.Value.Goods;
    export default {
        name: "ProductsComponetn",
        data() {
            return {
                namesJ,
                goods,
                rateUSD: 2.6,
                nId: 'Нет ID',
                BYN: 'руб.',
            }
        },
        methods: {
            openCloseTable: function (e) {
                e.path[1].classList.toggle("active");
                const a = e.path[2].querySelectorAll('.item');
                a.forEach(elem=>elem.classList.toggle("no-display"));
            },
        }
    }
</script>

<style lang="scss">
    @import "../variables.scss";
    .product-component {
        width: 50%;
        table {
            width: 100%;
            margin-bottom: 20px;
            border: 1px solid $color-border-table;
            border-radius: 5px;
        }
        th, td {
            padding: 0;
            border: 1px solid $color-border-table;
        }
        td {
            text-align: left;
        }
        h5 {
            display: inline;
            margin: 0;
            font-size: 12px;
        }
        span {
            font-size: 14px;
        }
        .name {
            background-color: $color-name-bg;
            color: $color-name;
            th {
                position: relative;
                &::before {
                    position: absolute;
                    width: 10px;
                    height: 10px;
                    top: 10px;
                    left: 10px;
                    content: url("../assets/ico/angle-arrow-down_icon-icons.com_73683.svg");
                    transform: scale(0.04) rotate(180deg);
                }
            }
        }
        .name.active {
            th {
                &::before {
                    transform: scale(0.04);
                    top:0;
                    left: 0;
                }
            }
        }
        .price {
            width: 20%;
            background-color: $color-price-bg;
            font-weight: bold;
            text-align: center;
        }
        .item {
            &:hover {
               background-color:$color-item-hover;
                cursor: pointer;
            }
        }
    }
</style>