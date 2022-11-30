<template>
	<div class="auth">
            <form class="form" @submit.prevent="auth">
					
                <div class="title_auth">Авторизация</div>
					<button @click="close">Закрыть</button>
                <div class="text">Введите логин</div>
                <input type="text" v-model="login">

                <div class="text">Введите пароль</div>
                <input type="text" v-model="password">
                <input type="submit">
            </form>
        </div>
</template>
<script>
import axios from 'axios'
export default {
	name: 'auth_block',
	methods: {
		async auth() {
            const {data} = await axios.post('http://localhost/backend/basic/web/index.php/api/auth-user?login='+this.login+'&password='+this.password)
            this.$emit('check', data)
				this.$emit('close', false)
        },
		close() {
			this.$emit('close', false)
		}
	}
}
</script>
<style>
.auth {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	background: rgba(0, 0, 0, 0.445);
	display: flex;
	justify-content: center;
	align-items: center;
}
.form {
	width: 800px;
	height: 500px;
	background: #256;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
input, button {
	width: 760px;
}
.title_auth {
font-size: 60px;
color: #fff;
}

</style>