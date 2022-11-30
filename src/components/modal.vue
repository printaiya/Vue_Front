<template>
<div class="wrap">
	new login:
	<form @submit.prevent="save">
		<input type="text" v-model="login">
		<input type="submit" value="submit">
	</form>
	
	<button @click="close">close</button>
</div>
</template>
<script>
import axios from 'axios'
export default {
	name: 'Modal_block',
	props: {
		valuesArray: Object
	},
	data() {
		return {
			login: this.valuesArray.login,
		}
	},
	methods: {
		save() {
			axios.post('http://localhost/backend/basic/web/index.php/api/update-data?id='+this.valuesArray.id+'&newvalue='+this.login)
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