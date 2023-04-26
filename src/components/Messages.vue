<template>
    <div>
        <h2>Mensajes</h2>
        <p v-for="message in messages" :key="message.id">
            Título: {{ message.title }}
            <br>
            Mensaje: {{ message.body }}
            <hr>
        </p>
    </div>
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
<style></style>