<template>
  <nav class="nav-main">
    <router-link class="nav-main-link" :to="{ name: 'Home' }"
      >Projects</router-link
    >
    <router-link class="nav-main-link" :to="{ name: 'AddProject' }"
      >Add a New Project</router-link
    >
  </nav>
</template>

<script>
export default {};
</script>

<style>
.nav-main {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 1rem;
  margin: 2rem 0;
}
a.nav-main-link {
  text-decoration: none;
  font-weight: bold;
  margin: 0 1rem;
}
a.nav-main-link:link,
a.nav-main-link:visited {
  color: var(--grey);
}
a.router-link-active {
    border-bottom: 3px solid var(--green);
}
</style>