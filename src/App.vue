<script >
import { RouterLink, RouterView } from 'vue-router'
export default {
  data() {
    return {
      isLoggedIn: false
    };
  },
}
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/register">Register</RouterLink>
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
  width: 100%;
  max-height: 100vh;

  grid-row: 1 / 2;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
  font-size: 12px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
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
