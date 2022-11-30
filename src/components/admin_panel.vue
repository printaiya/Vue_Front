<template>
<div>
                <table>
                    <tr>
                        <th>Заказ №<div class="icon"></div></th>

                        <th>Дата<div class="icon"></div></th>

                        <th>Покупатель<div class="icon"></div></th>

                        <th>Товар<div class="icon"></div></th>

                        <th>Количество<div class="icon"></div></th>

                        <th>Стоимость<div class="icon"></div></th>

                        <th>Итого<div class="icon"></div></th>

                    </tr>
                    <tr v-for="(item, key) in orders" :key="key">
                        <td>{{key+1}}</td>
                        <td>{{item.order_date}}</td>
                        <td>{{item.Full_name}}</td>
                        <td>{{item.title_product}}</td>
                        <td>{{item.quantity_of_order}}</td>
                        <td>{{item.price}}</td>
                        <td>{{item.price * item.quantity_of_order}}</td>
                    </tr>
                </table>
            </div>


            <div class="add">
            <button @click="regis">Добавить пользователя</button>
            </div>
            <div class="block" v-for="(items,key) in sortArray" :key="key">
            <div>{{items.login}}</div> <div><button class="delete" @click="deleteUser(key)" value="{{key}}">Delete</button><button @click="open(key)" value="{{key}}">edit</button></div>
        </div>
            <Modal_block :valuesArray="objectSend" @close="close" v-if="is_visible"></Modal_block>
            <regis_block  @close="close" v-if="is_regis"></regis_block>
            <button @click="logout">Выход</button>
  
</template>
<script>
import regis_block from '@/components/regis.vue'
import Modal_block from '@/components/modal.vue'
import axios from 'axios'
export default {
	name: 'admin_panel',
	data() {
		return {
			file: '',
            orders: [],
            users: [],
            sortArray: [],
            objectSend: {},
            is_regis: false,
            is_visible: false
		}
	},
    components: {
        Modal_block,
        regis_block,
    },
	methods: {
		async saveFile() {
            let Myformdata = new FormData()
            this.file = this.$refs.file.files[0];
            Myformdata.append('file', this.file)
            const {data} = await axios.get('http://localhost/backend/basic/web/index.php/api/upload-file', Myformdata)
            console.log(data);
        },
        open(key) {
            this.objectSend = this.sortArray[key]
            this.is_visible = true
        },
        async getOrders() {
            const {data} = await axios.get('http://localhost/backend/basic/web/index.php/api/get-orders')
            this.orders = data
            console.log(data);
        },
        deleteUser(key) {
            let id = this.sortArray[key].id
            axios.post('http://localhost/backend/basic/web/index.php/api/delete-data?id='+id)
        },
        regis() {
            this.is_regis = true
        },
        close(value) {
            this.is_regis = value
            this.is_visible = value
        },
        async getUsers() {
            const {data} = await axios.get('http://localhost/backend/basic/web/index.php/api/get-data')
            this.users = data
            this.sortArray = this.users
        },
        logout() {
            this.$emit('logout', true)
        }
	},
    mounted() {
    this.getUsers()
    this.getOrders()
}

}
</script>
<style scoped>
table {
    width: calc(100% - 20px);
    margin: 25px auto;
    border: 2px solid #000;
}
tr {
    width: 1200px;
    margin: 0 auto;
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}
td, th {
text-align: center;
width: 350px;
}
button {
    width: 250px;
}
.delete {
    color: #f00;
}
</style>