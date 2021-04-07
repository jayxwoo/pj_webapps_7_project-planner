<template>
  <NavMain />
  <router-view />
</template>

<script>
import NavMain from "./components/NavMain";

export default {
  components: { NavMain },
};
</script>

<style>
html {
  box-sizing: border-box;
  font-size: 16px;
  scroll-behavior: smooth;
}
body {
  background-color: var(--bglightgrey);
  min-height: 100vh;
}
*,
*::before,
*::after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}
:root {
  --black: rgba(20, 20, 20, 1);
  --darkgrey: rgba(70, 70, 70, 1);
  --grey: rgba(130, 130, 130, 1);
  --lightgrey: rgba(200, 200, 200, 1);
  --bglightgrey: rgba(235, 235, 235, 1);
  --green: rgba(0, 201, 138, 1);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeSpeed;
  line-height: 1.5;
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  color: var(--grey);
}
</style>
