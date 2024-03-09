<template>
    <div class="form-container">
        <form @submit.prevent="register" class="register-form">
            <input type="text" name="name" id="name" v-model="name" placeholder="Your name">
            <input type="email" name="email" id="email" v-model="email" placeholder="Your email">
            <input type="password" name="password" id="password" v-model="password" placeholder="Password">
            <button type="submit">Register</button>
        </form>
    </div>
</template>

<script>
    import axios from '@/axios'
    export default {
        data () {
            return {
                name: '',
                email: '',
                password: ''
            }
        },
        methods: {
            async register(){
                try {
                    const response = await axios.post('/register',{
                        name: this.name,
                        email: this.email,
                        password: this.password
                    });
                    console.log(response)
                } catch (error) {
                    console.error('An Error Occoure:', error);
                    if (error.response) {
                        console.error('Error Details:', error.response);
                    }
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
.register-form {
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
.register-form button {
    background-color: #007BFF;
    color: white;
    cursor: pointer;
}
</style>