<template lang="pug">
.container
  nav.navbar
    a.navbar-brand(href="/")
      font-awesome-icon(icon="home") Akinoriv
    .navbar-nav.mr-auto
      li.nav-item
        router-link.nav-link(v-if="currentUser" to="/user") User

    .navbar-nav.ml-auto(v-if="!currentUser")
      li.nav-item
        router-link.nav-link(to="/register")
          font-awesome-icon(icon="user-plus") Sign Up
      li.nav-item
        router-link.nav-link(to="/login")
          font-awesome-icon(icon="sign-in-alt") Login

    .navbar-nav.ml-auto(v-if="currentUser")
      li.nav-item
        router-link.nav-link(to="/profile")
          font-awesome-icon(icon="user") {{ currentUser.username }}
      li.nav-item
        a.nav-link(@click.prevent="logOut")
          font-awesome-icon(icon="sign-out-alt") LogOut
</template>

<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
import { useRouter } from "vue-router";

const store = useStore();
const router = useRouter();

const currentUser = computed(() => store.state.auth.user);

function logOut() {
  store.dispatch("auth/logout");
  router.push({
    name: "login",
  });
}
</script>

<style lang="scss" scoped>
.navbar {
  width: 100%;
  background: red;
  padding: 8px;
}
</style>
