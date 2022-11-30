<template>
	<div class="wrap">
		new login:
		<form @submit.prevent="save">
			<input type="text" v-model="login">
			<input type="password" v-model="password">
			<input type="submit" value="submit">
		</form>
		
		<button @click="close">close</button>
	</div>
	</template>
	<script>
	import axios from 'axios'
	export default {
		name: 'regis_block',
		data() {
			return {
				login: '',
				password: ''
			}
		},
		methods: {
			save() {
				axios.post('http://localhost/backend/basic/web/index.php/api/insert-data?login='+this.login+'&password='+this.password)
				this.$emit('close', false)
			},
			close() {
				this.$emit('close', false)
			}
		}
	}
	</script>
	<style>
	
	</style>