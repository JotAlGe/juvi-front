<script >
import { RouterLink, RouterView } from 'vue-router'
export default {
  data() {
    return {
      isLoggedIn: false,
      isAdmin: false
    };
  },
}
</script>

<template>
  <header>
    <div class="juvi-logo">
      <img src="././assets/images/juvi-horizontal.png" alt="logo juvi">
    </div>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink v-if="isLoggedIn ? false : true" to="/register">Register</RouterLink>
      <RouterLink v-if="isLoggedIn && (isAdmin ? false : true)" to="/contact">Contact</RouterLink>
      <RouterLink v-if="isLoggedIn && isAdmin" to="/messages">Messages</RouterLink>
      <router-link :to="isLoggedIn ? '/logout' : '/login'">
        {{ isLoggedIn ? 'Logout' : 'Login' }}
      </router-link>
    </nav>
  </header>
  <router-view></router-view>
</template>

<style>
header {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 100%;
  max-height: 100vh;

  grid-row: 1 / 2;
}

.juvi-logo {
  height: 6vh;
  max-height: 100%;
}

.juvi-logo img {
  max-height: 100%;
}

main {
  max-width: 100%;
  max-height: 90%;
  grid-row: 2 / 12;

  display: grid;
  place-items: center;
}

main div {
  height: 100%;
  width: 100%;
}

nav {
  font-size: 1rem;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 100%;
  height: 100%;
}

nav a {
  color: var(--color-brand-text)
}

nav a.router-link-exact-active {
  color: var(--color-brand-text-3);
}

nav a.router-link-exact-active:hover {
  border: none;
  background-color: var(--color-background);
}

nav a:hover {
  background-color: var(--color-background);
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    font-size: 1rem;

    padding: 1rem 0;
  }
}
</style>
