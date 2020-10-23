<template>
    <div class="rate">
        <label for="rateUSD">{{rateText}}</label>
        <input id="rateUSD" type="text" :value="rateUSD" v-on:change="getRate()">
    </div>
    <div class="product-component">
        <table v-for="(name, idx) in namesJ" :key="idx">
            <tr class="name-group" v-on:click="openCloseTable">
                <th colspan="3">{{name.G}}</th>
            </tr>
            <tr class="item" v-for="(nameB, idx) in name.B" :key="idx" :data-id="nameB.T">
                <td class="name-product-qty">
                    <h5>{{nameB.N}}</h5>
                    <span v-for="(good, idx) in goods" :key="idx">
                            <span v-if="good.T === nameB.T">({{good.P}})</span>
                        </span>
                </td>
                <td class="price">
                    <span v-if="nameB.T==''">{{nId}}</span>
                    <span v-else v-for="(good, idx) in goods" :key="idx">
                            <span v-if="good.T === nameB.T">{{(good.C * rateUSD).toFixed(2)}} {{BYN}}</span>
                      </span>
                </td>
                <td class="add-to-cart">
                    <button v-on:click="productToCart()"> +</button>
                </td>
            </tr>
        </table>
    </div>
    <div class="cart">
        <table>
            <tr>
                <th class="name-text">{{nameText}}</th>
                <th class="qty-text">{{qtyText}}</th>
                <th class="price-text">{{priceText}}</th>
                <th></th>
                <th></th>
            </tr>
            <tr class="item-cart" v-for="(item, idx) in this.arrayCart" :key="idx" :data-id="idx">
                <td>{{item.productName}}</td>
                <td class="qty">
                    <div class="qty-box">
                        <input type="text" :value="item.productQtyInCat"
                               v-on:change="checkValueInput(item, item.productQty)">
                        <span class="ed">{{ed}}</span>
                        <button class="add-cart" v-on:click="addInputVal(item)">+</button>
                        <button class="remove-cart" v-on:click="removeInputVal(item)">-</button>
                    </div>
                    <div class="mess" v-if="item.productQty <= minQtyVal "><span>{{mess}}</span></div>
                </td>
                <td class="item-cart__price">
                    <span>{{(item.productPrice).toFixed(2)}} {{BYN}}<span class="ed">&nbsp;/ {{ed}}</span></span>
                </td>
                <td class="del-cart-box">
                    <button class="del-cart" v-on:click="removeProduct(2)">{{delText}}</button>
                </td>
            </tr>
            <tr>
                <th class="sum-box" colspan="4" ><span class="sum">{{sumText}}</span><span class="sum-val">{{getSum().toFixed(2)}} {{BYN}}</span></th>
            </tr>
        </table>
    </div>
</template>
<script>
    import dataJ from '../assets/tets/data.json';
    import namesJ from '../assets/tets/names.json';

    const goods = dataJ.Value.Goods;

    export default {
        name: "ProductsComponetn",
        data() {
            return {
                namesJ,
                goods,
                rateUSD: 20,
                rateText:"Введите курс от 20 до 80:",
                nId: 'Нет ID',
                BYN: 'руб.',
                nameText: 'Наименование товара и описание',
                priceText: 'Цена',
                qtyText: 'Колличество',
                delText: 'Удалить',
                sumText: 'Общая стоимость: ',
                mess: 'Колличество ограничено',
                ed: "шт",
                sumVal: 0,
                arrayCart: [],
                minQtyVal: 1,
                url: 'https://www.cbr-xml-daily.ru/daily_json.js',
                time: 1500,
            }
        },
        methods: {
            openCloseTable: function (e) {
                //механизм скрытия не нужных категорий (итегрировать уже написанные сложнее чем написать новый)
                e.path[1].classList.toggle("active");
                const a = e.path[2].querySelectorAll('.item');
                a.forEach(elem => elem.classList.toggle("no-display"));
            },
            productToCart: function () {
                //создаю переменные для формирования масива корзины
                const item = event.target.parentElement.parentElement;
                const id = item.dataset.id;

                if (!id) {
                    //заглушка потому что в исходных данных не визде корректно внесены id (T);
                    return alert("Сожалею не у выбранного вами товара нет ID");
                }

                // потому что T(id) задублированы и не совпадают так бы сравнивал имена по id
                const productName = item.querySelector('.name-product-qty').querySelector('h5').innerText;
                const thisProduct = this.goods.filter(elem => elem.T == id)[0];
                const productQty = thisProduct.P;
                const productPrice = thisProduct.C * this.rateUSD;
                let productQtyInCat = 1;

                // создаю новый масив для управления корзиной
                const newElem = {id, productName, productQty, productPrice, productQtyInCat};

                // сравниваю нет ли такого товара в карсине (масиве)
                function contains(arr, elem) {
                    for (var i = 0; i < arr.length; i++) {
                        if (arr[i].productName === elem.productName) {
                            return true;
                        }
                    }
                    return false;
                }

                // если такого товара нет то добавляю если есть то говорю клиенту что он уе в корзине
                if (contains(this.arrayCart, newElem)) {
                    alert("Товар уже добавлен в корзину");
                } else {
                    this.arrayCart.push(newElem);
                }

            },
            addInputVal: function (array) {
                // проверяю колличество имеющегося товара и не разрешаю добавть если превышено.
                if (array.productQty > array.productQtyInCat) {
                    array.productQtyInCat++;
                } else {
                    alert("Превышено максимальное колличество товара");
                }
            },
            removeInputVal: function (array) {
                //добавляю возможность отнять колличество товара и убираю из карзины если колличество меньше 0
                if (array.productQty >= array.productQtyInCat) {
                    if (array.productQtyInCat !== 1) {
                        array.productQtyInCat--;
                    } else {
                        this.removeProduct(3);
                    }
                }
            },
            getSum: function () {
                //получаю сумму товаров в карзине
                const result = this.arrayCart.reduce((a, b) => a + b.productPrice * b.productQtyInCat, 0);
                return result;
            },
            checkValueInput: function (item, qty) {
                //слежу за изменениями инпута по колличеству
                if (qty < Number(event.target.value)) {
                    alert(`Не хватает необходимого колличества товара, максимальное колличество товара: ${qty} шт`);
                    event.target.value = qty;
                } else {
                    item.productQtyInCat = Number(event.target.value);
                }

            },
            removeProduct: function (qtyParent) {
                if (qtyParent === 3) {
                    this.arrayCart.splice(event.target.parentElement.parentElement.parentElement.dataset.id, 1);
                } else {
                    this.arrayCart.splice(event.target.parentElement.parentElement.dataset.id, 1);
                }
            },
            getRate: function () {

                if (Number(event.target.value) >= 20 && Number(event.target.value) <= 80) {
                    this.rateUSD = Number(event.target.value);
                }else {
                    alert("Превышен максимально возможный предел курса ввалюты");
                }

            }
        },
    }
</script>

<style lang="scss">
    @import "../variables.scss";
    .rate {
        width: 100%;
        margin-bottom: 100px;
        label {
           padding-right: 10px;
        }
        #rateUSD {
            width: 2%;
        }
    }
    .button-primary {
        all: unset;
        text-align: center;
        background: $color-button-bg;
        color: white;
        border: 1px solid ghostwhite;
        cursor: pointer;
        &:hover {
            background: $color-button-hover-bg;
        }
        &:active {
            border: 1px solid black;
        }
    }
    .product-component {
        width: 50%;
        box-sizing: border-box;
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
        .name-group {
            background-color: $color-name-bg;
            color: $color-name;
            cursor: pointer;
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
        .name-group.active {
            th {
                &::before {
                    transform: scale(0.04);
                    top: 0;
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
                background-color: $color-item-hover;
                cursor: pointer;
            }
        }
        .add-to-cart {
            display: flex;
            justify-content: center;
            button {
                width: 31px;
                height: 100%;
                margin: 10px;
                @extend .button-primary;
            }
        }
    }
    .cart {
        width: 50%;
        box-sizing: border-box;
        padding: 10px;
        .name-text, .qty-text, .price-text {
            padding: 13px 0;
            color: $color-cart-text;
            font-weight: 500;
        }
        th, td {
            text-align: left;
        }
        table {
            font-size: 12px;
            border-collapse: collapse
        }
        .item-cart {
            padding: 16px 0 14px 0;
            border-top: 1px solid $color-border-cart;
            &__price {
                padding-top: 16px;
                min-width: 125px;
                display: flex;
                font-weight: bold;
            }
        }
        .qty {
            .qty-box {
                padding: 16px 0 14px 0;
                display: flex;
                input {
                    width: 35%;
                    margin-bottom: 5px;
                    border-radius: 0;
                    border: 1px solid $color-border-input;
                }
                span {
                    width: 25%;
                    text-align: center;
                }
                button {
                    @extend .button-primary;
                    width: 10%;
                }
            }
            .mess {
                width: 77%;
                text-align: center;
                border: 1px dotted $color-mess-border;
                background-color: $color-mess-bg;
                color: $color-mess-color;
                padding: 8px 5px;
                font-size: 0.7em;
            }
        }
        .name {
            width: 60%;
        }
        .del-cart-box {
            vertical-align: text-top;
            .del-cart {
                all: unset;
                cursor: pointer;
            }
        }

        .ed {
            color: $color-cart-text;
        }
        .sum-box {
            text-align: right;
            .sum {
                color: $color-cart-text;
                text-align: right;
                padding-right: 10px;
                font-weight: normal;
            }
            .sum-val {
                color: $color-mess-color;
            }
        }
    }
</style>