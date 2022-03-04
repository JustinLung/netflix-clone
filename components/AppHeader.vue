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
    <input type="search" class="search" placeholder="🍿 Search Movie..." />
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

.search {
  border: none;
  height: 2.25em;
  width: 2.25em;
  border-radius: 1.125em;
  padding-left: 2.25em;

  background: url("~assets/search.svg") no-repeat 0.625em/1em, var(--white);
  cursor: pointer;

  transition-property: width, border-radius, box-shadow;
  transition-duration: 300ms;
}

.search:focus {
  width: 12.5em;
  border-radius: 0.25em;
  box-shadow: 0 0 0 2px var(--red);
  cursor: auto;
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
