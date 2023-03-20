<!--  'http://127.0.0.1:80/api/auth/register'-->
<template>
    <div>
        <h1>Registro de usuario</h1>
        <form @submit.prevent="register">
            <label>
                Nombre:
                <input type="text" v-model="name">
            </label>
            <br>
            <label>
                Apellido:
                <input type="text" v-model="lastname">
            </label>
            <br>
            <label>
                Email:
                <input type="email" v-model="email">
            </label>
            <br>
            <label>
                Contraseña:
                <input type="password" v-model="password">
            </label>
            <br>
            <button type="submit">Registrar</button>
        </form>
        <p v-if="mess">{{ mess }}</p>
        <p v-if="errors">{{ errors }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            lastname: '',
            email: '',
            password: '',
            mess: '',
            errors: ''
        };
    },
    methods: {
        async register() {
            const userData = {
                name: this.name,
                lastname: this.lastname,
                email: this.email,
                password: this.password
            };

            fetch('http://127.0.0.1:80/api/auth/register', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(userData)
            })
                .then(response => response.json())
                .then(data => {
                    // console.log(data.data.message)
                    this.mess = data.data.message;
                    this.errors = '';
                    this.name = '';
                    this.lastname = '';
                    this.email = '';
                    this.password = '';
                })
                .catch(error => {
                    this.mess = '';
                    this.errors = 'Faltan completar campos';
                    // this.errors = error
                    // console.log(this.error);
                });
        }
    }
};
</script>
