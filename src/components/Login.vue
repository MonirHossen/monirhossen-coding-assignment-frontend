<template>
    <div class="container">
        <form @submit.prevent="login" class="login-form">
            <input type="email" name="email" placeholder="Email.." v-model="email" />
            <input type="password" name="password" placeholder="Password.." v-model="password" />
            <button type="submit">LogIn</button>
        </form>
    </div>
</template>

<script>
import axios from '@/axios'
export default {
    data () {
        return {
            email: "",
            password: ""
        }
    },
    methods: {
        async login() {
            try {
                const response = await axios.post('/login',{
                    email: this.email,
                    password: this.password
                });

                if (response.data.token) {
                    localStorage.setItem('token', response.data.token)

                    this.$store.commit('LOGIN');

                    this.$router.push('/')
                }

            } catch (error) {
                console.error('An error occurred')
            }
        }
    }
}
</script>