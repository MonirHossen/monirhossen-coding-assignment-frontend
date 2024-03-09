<template>
    <div class="form-container">
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

<style scoped>
/* styling for the outer form container */
.form-container {
    display: flex;
    justify-content: center;
    align-items: center;
}
/* styling for the login form layout and apperance */
.login-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 300px;
    padding: 20px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 16px;
}
/* Specific styling for login button */
.login-form button {
    background-color: #007BFF;
    color: white;
    cursor: pointer;
}
</style>