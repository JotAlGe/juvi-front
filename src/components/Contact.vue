<template>
    <div class="contact_section layout_padding">
        <div class="container">
            <h1 class="work_taital">Contacto</h1>
        </div>
    </div>

    <div v-if="mess" class="success">{{ mess }}</div>
    <div v-else style="color:red;">{{ err }}</div>

    <div v-if="isLoading" class="loader"></div>
    <div v-else class="contact_section_2">
        <div class="col-md-6 padding_0">
            <div><img src="src/assets/images/img-10.png" class="image_10"></div>
        </div>
        <div class="container-fluid">
            <div class="row">
                <div class="col-md-6">
                    <form class="email_text" @submit.prevent="sendMessage">
                        <div class="form-group">
                            <input type="text" class="email-bt" placeholder="Escribe un título..." name="title"
                                v-model="title">
                        </div>
                        <div class="form-group">
                            <textarea class="massage-bt" placeholder="Massage" rows="5" id="comment" name="Massage"
                                v-model="body"></textarea>
                        </div>
                        <div class="send_btn"><button @click="sendMessage" type="button">SEND</button></div>
                    </form>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
import jwt_decode from 'jwt-decode';
export default {
    data() {
        return {
            title: '',
            body: '',
            mess: '',
            err: '',
            isLoading: false
        }
    },
    methods: {
        async sendMessage() {
            const token = localStorage.getItem('token');
            const decodedToken = jwt_decode(token);
            const userId = decodedToken.sub;

            const messageData = {
                title: this.title,
                body: this.body,
                user_id: userId
            }

            this.isLoading = true;

            fetch('http://127.0.0.1:80/api/messages', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json',
                    'Authorization': `Bearer ${localStorage.getItem('token')}`
                },
                body: JSON.stringify(messageData)
            })
                .then(response => response.json())
                .then(data => {

                    this.mess = data.message;

                    this.title = ''
                    this.body = ''
                    this.isLoading = false
                })
                .catch(error => {
                    this.isLoading = false
                    this.err = error;
                })
        }
    }
}
</script>
<style>
.success {
    color: green;
    text-align: center;
}

.error {
    color: red;
    text-align: center;
}

.send_btn {
    width: 100px;
    height: 30px;
}

.send_btn button {
    width: 100%;
    height: 100%;
    border: none;
    background-color: #262525;
    color: white;
}

.send_btn button:hover {
    background-color: #fff;
    color: #262525;
    border: 1px solid rgba(38, 37, 37);
}

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
</style>