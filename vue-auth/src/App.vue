<template>
  <div id="app">
    <sidebar />

    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script setup>
import Sidebar from "./views/sidebar.vue";
</script>
