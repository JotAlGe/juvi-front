<template>
    <div>
        <h1 class="logout">Logging out...</h1>
    </div>
</template>
<script>
export default {
    mounted() {
        fetch('http://127.0.0.1:8000/api/auth/logout', {
            method: 'POST',
            headers: {
                Authorization: `Bearer ${localStorage.getItem('token')}`
            }
        })
            .then(response => response)
            .then(data => {
                this.$root.isLoggedIn = false;
                localStorage.removeItem('token');
                this.$router.push('/login');
                this.$root.isAdmin = false
            })
            .catch(error => console.log(error))
    }
}
</script>
<style>
.logout {
    text-align: center;
}
</style>