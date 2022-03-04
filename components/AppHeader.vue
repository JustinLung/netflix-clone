<template>
  <header>
    <NuxtLink to="/"
      ><img src="~assets/netflix-logo.png" class="logo" alt="Netflix Logo"
    /></NuxtLink>
    <nav>
      <ul>
        <li><NuxtLink to="/">Home</NuxtLink></li>
        <li><NuxtLink to="/Series">Series</NuxtLink></li>
        <li><NuxtLink to="/Movies">Movies</NuxtLink></li>
      </ul>
    </nav>
  </header>
</template>
<script>
export default {};
</script>
<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1em 2.5em;
  position: fixed;
  z-index: 99;
  width: 100%;
}

.logo {
  width: 8em;
}

nav {
  flex-grow: 1;
}

ul {
  display: flex;
  gap: 2em;
}

ul li > a {
  color: var(--white);
  cursor: pointer;
}

@media (max-width: 40em) {
  header {
    padding: 1em;
  }
}
</style>
