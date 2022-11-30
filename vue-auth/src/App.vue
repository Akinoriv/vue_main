<template lang="pug">
.app(id="app")
  sidebar

  .container
    router-view
</template>

<script setup>
import Sidebar from "./views/sidebar.vue";
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Playfair+Display&display=swap");

html,
body {
  font-family: "Playfair Display", serif;
}

#app {
  font-family: "Playfair Display", serif;
}

.app {
  background: url(./assets/white-fon.jpg) center no-repeat;
  background-size: cover;
  min-height: 100vh;
}
</style>
