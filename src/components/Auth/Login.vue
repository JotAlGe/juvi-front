<template>
    <div class="log-form">
        <h2>Iniciar sesión</h2>
        <form @submit.prevent="login">
            <input type="email" placeholder="email" v-model="email" />
            <input type="password" placeholder="password" v-model="password" />
            <button type="submit" class="btn">Login</button>
            <a class="forgot" href="#">Forgot Username?</a>
            <div v-if="err"> {{ err }} </div>
        </form>
    </div><!--end log form -->
</template>
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            err: ''
        }
    },
    methods: {
        login() {
            const loginData = {
                email: this.email,
                password: this.password
            }

            fetch('http://127.0.0.1:80/api/auth/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                },
                body: JSON.stringify(loginData)
            })
                .then(response => {
                    if (response.ok) {
                        return response.json();
                    } else {
                        throw Error('No se pudo autenticar...');
                    }
                })
                .then(data => {
                    this.email = ''
                    this.password = ''
                    this.$router.push('/dashboard')
                    // console.log(data)
                })
                .catch(error => {
                    this.err = error
                    // console.log(this.err)
                })
        }
    }
}
</script>
<style></style>
