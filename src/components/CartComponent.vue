<template>
    <div class="cart">
        <div class="popup">
            <h3></h3>
        </div>
        <table>
            <tr>
                <th class="name">{{nameText}}</th>
                <th>{{qtyText}}</th>
                <th>{{priceText}}</th>
                <th></th>
            </tr>
            <tr>
                <td>Ячейка 3</td>
                <td>Ячейка 4</td>
                <td>Ячейка 4</td>
                <td>{{delText}}</td>
            </tr>
        </table>

    </div>
</template>

<script>
    export default {
        name: "CartComponent",
        data() {
            return {
                nameText:'Наименование товара и описание',
                priceText: 'Цена',
                qtyText:'Колличество',
                delText:'Удалить',
            }
        },
    }

    document.addEventListener("DOMContentLoaded", () => {
        document.querySelectorAll('.item').forEach(elem=>elem.addEventListener('click', function () {
            console.log(123)
            // let name = this.querySelectorAll('h5')[0].innerText;
            // let id = this.dataset.id;
            // this.data.arrayCart.push({name, id});
        }));
    });
</script>

<style lang="scss">
    .cart {
        th, td {
            text-align: left;
        }
        width: 50%;
        table {
            font-size: 12px;

        }
        .name {
            width: 60%;
        }
    }
</style>