<template>
    <div>
        <h1>Logging out...</h1>
    </div>
</template>
<script>
export default {
    mounted() {
        fetch('http://127.0.0.1:80/api/auth/logout', {
            method: 'POST',
            headers: {
                Authorization: `Bearer ${localStorage.getItem('token')}`,
            },
        })
            .then(response => response.json())
            .then(data => {
                this.$root.isLoggedIn = false;
                localStorage.removeItem('token');
                this.$router.push('/login');
            })
            .catch(error => console.error(error));
    }
}
</script>
<style></style>