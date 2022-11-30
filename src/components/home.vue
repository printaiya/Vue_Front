<template>
    <div class="wrapper">
       <div class="products">
        <div class="flex" v-for="(item, key) in products" :key="key">
            <div class="img">
                <img :src="item.img" alt="">
            </div>
           <div class="container">
                <div class="title">{{item.title_product}}</div>
                <div class="price">{{item.price}}</div>
                <div class="justify">
                    <button>Подробнее</button>
                    <button class="btn"><div class="icon-like"></div></button>
                </div>
           </div>
        </div>
       </div>
    </div>
</template>
<script>
import axios from 'axios'


export default {
    name: "home_page",
    data() {
        return {
            users: [],
            orders: [],
            products: []
        }
    },
    methods: {
        async getProducts() {
            const {data} = await axios.get('http://localhost/backend/basic/web/index.php/api/get-products')
            this.products = data
        }
},
mounted() {
    this.getProducts()
},
}

</script>
<style scoped>
.wrapper {
    padding: 15px;
}
.add {
    display: flex;
    height: auto;
    align-items: center;
    margin-bottom: 15px;
    margin-left: 15px;
}
.large {
    width: 140px;
}
.add div {
    margin-right: 25px;
}
* {
    color: #fff;
}
input {
    color: #000;
}
.block {
    margin-left: 15px;
    width: 600px;
    height: 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #000;
}

.admin {
    padding-left: 15px;
    margin-top: 15px;
}
.search {
    margin-left: 15px;
}
.profile {
    width: 600px;
    height: 200px;
    margin-top: 15px;
    border: 1px solid #000;
}
.title {
    font-size: 40px;
}
.products {
    width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
}
.flex {
    width: 500px;
    height: 800px;
    background: rgb(17, 75, 102);
    display: flex;
    flex-direction: column;
    margin-top: 40px;
}
.container {
    padding: 15px;
}
.img {
    width: 500px;
    height: 600px;
}
.justify {
    display: flex;
    width: 500px;
    justify-content: space-between;
}
img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
.price {
    font-size: 25px;
}
button {
    background: transparent;
    border: 0;
    max-width: 50px;
}
.icon-like {
    width: 50px;
    height: 50px;
    background-image: url('../icons/favorite-5-multi-size\ \(1\).ico');
    background-size: cover;
}
</style>