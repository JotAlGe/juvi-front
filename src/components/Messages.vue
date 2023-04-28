<template>
    <h2>Mensajes</h2>
    <p v-for="message in messages" :key="message.id">
        <label for="">Título:</label> {{ message.title }}
        <br>
        <label for="">Mensaje:</label> {{ message.body }}
        <hr>
    </p>
</template>
<script>
export default {

    data() {
        return {
            messages: []
        }
    },
    mounted() {
        fetch('http://127.0.0.1:8000/api/messages', {
            headers: {
                Authorization: `Bearer ${this.$root.tok}`,
            },
        })
            .then((response) => response.json())
            .then((data) => {
                this.messages = data;
                console.log(this.messages)
            })
            .catch((error) => {
                console.error(error);
            });
    },
}
</script>
<style>
label {
    font-weight: bold;
    color: #252626;
}

p {
    font-weight: 400;
}
</style>