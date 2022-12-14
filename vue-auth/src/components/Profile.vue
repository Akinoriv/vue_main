<template lang="pug">
.profile(v-if="!isEdit")
  .header
    Person.person(:personaje="JSON.parse(currentUser.personaje)")
    h3
      strong Profile {{ currentUser.username }}
  p.field
    strong Id: 
    | {{ currentUser.id }}
  
  p.field
    strong Email: 
    | {{ currentUser.email }}

  p.field
    strong Token: 
    | {{ currentUser.accessToken.substring(0, 20) }}... 
  
  p.field
    strong(v-for="role in currentUser.roles" :key="role") Authorities: {{ role }}
  button.btn.field(@click="isEdit = true") edit
.profile.profile-edit(v-if="isEdit")
  Person-constructor(:personaje="currentUser.personaje")
  input(v-model="currentUser.username").field
  button.btn.field(@click="isEdit = false") save

</template>

<script setup>
import Person from "./Person.vue";
import PersonConstructor from "./PersonConstructor.vue";

import { computed, ref } from "vue";
import { useStore } from "vuex";
import { useRouter } from "vue-router";

const store = useStore();
const router = useRouter();

const currentUser = computed(() => store.state.auth.user);

let isEdit = ref(false);

if (!currentUser.value) {
  router.push("/login");
}
</script>

<style lang="scss" scoped>
.profile {
  margin: 20px auto;
  padding: 20px;
  max-width: 400px;
  border-radius: 10px;
  background-color: #ffeb5f30;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.9);
  display: flex;
  flex-direction: column;
}

.header {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.profile-edit {
}

.person {
  margin: 20px;
  border-radius: 10px;
}
.field {
  margin-top: 0;
  margin-bottom: 1rem;
  padding: 10px;
  background: gold;
  border-radius: 10px;
  color: rgb(67, 43, 0);
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.9);
  text-transform: uppercase;
}

.btn {
  width: 100px;
  border-radius: 10px;
  background: rgb(255 214 53);
  text-transform: uppercase;
  color: rgb(67, 43, 0);
  font-size: 20px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.9);
}
</style>
