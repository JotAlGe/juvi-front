<template>
    <div>
        <h1>Registro de usuario</h1>
        <form @submit.prevent="register" class="form">
            <div class="name">
                <input type="text" v-model="name" placeholder="Nombre...">
            </div>
            <br>
            <div class="lastname">
                <input type="text" v-model="lastname" placeholder="Apellido...">
            </div>
            <br>
            <div class="email">
                <input type="email" v-model="email" placeholder="Correo...">
            </div>
            <br>
            <div class="password">
                <input type="password" v-model="password" placeholder="Contraseña...">
            </div>
            <br>
            <button type="submit" class="register">Registrar</button>
        </form>
        <p v-if="mess">{{ mess }}</p>
        <p v-if="errors" class="error">{{ errors }}</p>
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
<style>
.error {
    color: red;
    text-align: center;
}

h1 {
    text-align: center;
}

.form {
    height: 80%;
    margin-top: 5%;
    display: grid;
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    grid-template-rows: repeat(5, 1fr);
}

label {
    font-weight: bold;
}

input {
    width: 100%;
    height: 5vh;
    border: none;
    border-bottom: 1px solid #252525;
}

.name {
    grid-column: 2 / 3;
}

.lastname {
    grid-column: 2 / 3;
    grid-row: 2 / 3;
}

.email {
    grid-column: 2 / 3;
    grid-row: 3 / 4;
}

.password {
    grid-column: 2 / 3;
    grid-row: 4 / 5;
    margin: auto;
}

.register {
    width: 170px;
    margin: auto;

    border: 1px solid #262525;
    background-color: #05141f;
    color: #fff;
    font-size: 16px;
    padding: 10px 0px;
    text-transform: uppercase;
    grid-column: 2 / 3;
    grid-row: 5 / 6;
}

.register:hover {
    color: #262525;
    background-color: #fff;
    border: 1px solid #262525;
}

@media screen and(max-width: 520px) {
    .form {
        width: 100%;
        height: 80%;
        margin-top: 5%;
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: repeat(5, 1fr);
    }

    .name,
    .email,
    .lastname,
    .password {
        grid-column-end: 2;
    }
}
</style>