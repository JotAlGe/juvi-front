<template>
    <div v-if="isLoading" class="loader"></div>
    <div v-else class="log-form">
        <h1>Iniciar sesión</h1>
        <form @submit.prevent="login" class="form">
            <input type="email" placeholder="Correo..." v-model="email" class="email" />
            <input type="password" placeholder="Contraseña..." v-model="password" class="password" />
            <button type="submit" class="btn">Login</button>
            <!-- <a class="forgot" href="#">Forgot Username?</a> -->
        </form>
        <p v-if="err" class="err"> {{ err }} </p>
    </div>
    <!--end log form -->
</template>
<script>
export default {

    data() {
        return {
            email: '',
            password: '',
            err: '',
            isLoading: false
        }
    },
    methods: {
        login() {
            const loginData = {
                email: this.email,
                password: this.password
            }

            this.isLoading = true

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
                    localStorage.setItem('token', data.access_token);
                    this.$root.isLoggedIn = true
                    this.$router.push('/')

                    // console.log(data)
                })
                .catch(error => {
                    this.err = error
                    this.isLoading = false

                })
        }
    }
}
</script>
<style>
.loader {
    color: #262525;
    font-size: 45px;
    text-indent: -9999em;
    overflow: hidden;
    width: 1em;
    height: 1em;
    border-radius: 50%;
    position: relative;
    z-index: 100;
    transform: translateZ(0);
    animation: mltShdSpin 1.7s infinite ease, round 1.7s infinite ease;
}

.btn {
    width: 170px;
    margin: auto;

    border: 1px solid #262525;
    background-color: #05141f;
    color: #fff;
    font-size: 16px;
    padding: 10px 0px;
    text-transform: uppercase;
}

.btn:hover {
    color: #262525;
    background-color: #fff;
    border: 1px solid #262525;
}

.err {
    color: red;
    text-align: center;

    grid-column: 2 / 3;
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

.email {
    grid-column: 2 / 3;
    grid-row: 2 / 3;
}

.password {
    grid-column: 2 / 3;
    grid-row: 3 / 4;
}

.btn {
    grid-column: 2 / 3;
    grid-row: 5 / 6;
}


@keyframes mltShdSpin {
    0% {
        box-shadow: 0 -0.83em 0 -0.4em,
            0 -0.83em 0 -0.42em, 0 -0.83em 0 -0.44em,
            0 -0.83em 0 -0.46em, 0 -0.83em 0 -0.477em;
    }

    5%,
    95% {
        box-shadow: 0 -0.83em 0 -0.4em,
            0 -0.83em 0 -0.42em, 0 -0.83em 0 -0.44em,
            0 -0.83em 0 -0.46em, 0 -0.83em 0 -0.477em;
    }

    10%,
    59% {
        box-shadow: 0 -0.83em 0 -0.4em,
            -0.087em -0.825em 0 -0.42em, -0.173em -0.812em 0 -0.44em,
            -0.256em -0.789em 0 -0.46em, -0.297em -0.775em 0 -0.477em;
    }

    20% {
        box-shadow: 0 -0.83em 0 -0.4em, -0.338em -0.758em 0 -0.42em,
            -0.555em -0.617em 0 -0.44em, -0.671em -0.488em 0 -0.46em,
            -0.749em -0.34em 0 -0.477em;
    }

    38% {
        box-shadow: 0 -0.83em 0 -0.4em, -0.377em -0.74em 0 -0.42em,
            -0.645em -0.522em 0 -0.44em, -0.775em -0.297em 0 -0.46em,
            -0.82em -0.09em 0 -0.477em;
    }

    100% {
        box-shadow: 0 -0.83em 0 -0.4em, 0 -0.83em 0 -0.42em,
            0 -0.83em 0 -0.44em, 0 -0.83em 0 -0.46em, 0 -0.83em 0 -0.477em;
    }
}

@keyframes round {
    0% {
        transform: rotate(0deg)
    }

    100% {
        transform: rotate(360deg)
    }
}
</style>
