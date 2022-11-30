<template lang="pug">
nav.navbar 
  .container
    a.navbar-brand(href="/")

    .navbar-nav.navbar-box(v-if="!currentUser")
      li.navbar-item
        router-link.navbar-link(to="/register")
          font-awesome-icon.navbar-link-icon(icon="user-plus") 
          .navbar-link-text Sign Up
      li.navbar-item
        router-link.navbar-link(to="/login")
          .navbar-link-icon(data-icon="ei-user")
          //- font-awesome-icon.navbar-link-icon(icon="sign-in-alt") 
          .navbar-link-text Login

    .navbar-nav.navbar-box(v-if="currentUser")
      li.navbar-item
        router-link.navbar-link(to="/profile")
          font-awesome-icon.navbar-link-icon(icon="user") 
          .navbar-link-text {{ currentUser.username }}
      li.navbar-item
        a.navbar-link(@click.prevent="logOut")
          font-awesome-icon.navbar-link-icon(icon="sign-out-alt") 
          .navbar-link-text LogOut
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
a {
  color: #5b5b5b;
}
.navbar {
  width: 100%;
  padding: 8px;
  background: gainsboro;
  color: gray;

  &-brand {
    background: url(../assets/logo.png) center no-repeat;
    background-size: contain;
    width: 4em;
    height: 1em;
  }

  &-box {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 0 4px;
  }

  &-link {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-left: 6px;
    padding: 0 4px;
    cursor: pointer;

    &-text {
      margin-left: 6px;
    }

    &-icon {
      max-height: 14px;
      max-width: 14px;
    }
  }
}
</style>
