<template>
	<button @click="open">Вход</button>
	<div class="wrapper" v-if="is_guest">
		<home_page ></home_page>
	</div>
	<admin_panel @logout="logout" v-if="is_admin"></admin_panel>
	
	<auth_block @close="close" @check="auth" v-if="is_auth"></auth_block>
</template>
<script>
import auth_block from '@/components/auth.vue'
import admin_panel from '@/components/admin_panel.vue'
import home_page from '@/components/home.vue'
export default {
	name: "main_page",
	data() {
		return {
			is_admin: false,
			is_manager: false,
			is_customer: false,
			is_guest: true,
			is_auth: false
		}
	},
	components: {
		auth_block,
		admin_panel,
		home_page
	},
	methods: {
		auth(object) {
			this.is_guest = false
			console.log(object);
			let role = object.role
			console.log(role);
			switch(role) {
				case 4: 
					
					break
				case 1:
					this.is_admin = true
					break
				case 2:
					this.is_manager = true
					break
				case 3: 
					this.is_customer = true
					break
				default:
					this.error = object	 
			}
		},
		close(value) {
			this.is_auth = value
			document.body.style.overflow = 'auto'
		},
		open() {
			this.is_auth = true
			document.body.style.overflow = 'hidden'
		},
		logout(value) {
			this.is_guest = value
			this.is_admin = !value
			this.is_manager = !value
			this.is_customer = !value
		}
	}
}
</script>
<style>
button {
	min-width: 150px;
}

</style>