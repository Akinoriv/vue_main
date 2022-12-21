<template lang="pug">
.container
  Person(:personaje="changedPersonaje")
  // TODO: add v-for for changedPersonaje
  .nav
    .nav-block
      font-awesome-icon.icon.icon-prev(icon="arrow-left" @click="prev('face', 11)")
      font-awesome-icon.icon.icon-center(icon="meh-blank")
      font-awesome-icon.icon.icon-next(icon="arrow-right" @click="next('face', 11)")
    .nav-block
      font-awesome-icon.icon.icon-prev(icon="arrow-left" @click="prev('eyes', 11)")
      font-awesome-icon.icon.icon-center(icon="eye")
      font-awesome-icon.icon.icon-next(icon="arrow-right" @click="next('eyes', 11)")
    .nav-block
      font-awesome-icon.icon.icon-prev(icon="arrow-left" @click="prev('rot', 12)")
      .icon.icon-center lips
      font-awesome-icon.icon.icon-next(icon="arrow-right" @click="next('rot', 12)")
</template>

<script setup>
import Person from "./Person.vue";
import { ref, toRefs, defineProps, defineEmits } from "vue";

const props = defineProps({
  personaje: {
    type: Object,
  },
});

const emit = defineEmits();

const { personaje } = toRefs(props);

let changedPersonaje = ref();

console.log(personaje.value);

if (personaje.value === null) {
  changedPersonaje.value = {
    face: Math.floor(Math.random() * 11) + 1,
    cheeks: Math.floor(Math.random() * 2) + 1,
    eyes: Math.floor(Math.random() * 11) + 1,
    rot: Math.floor(Math.random() * 12) + 1,
  };
  emit("personaje", changedPersonaje.value);
} else {
  changedPersonaje.value = JSON.parse(personaje.value);
}

function prev(item, length) {
  if (changedPersonaje.value[item] === 1) {
    changedPersonaje.value[item] = length;
  } else {
    changedPersonaje.value[item]--;
  }
  emit("personaje", changedPersonaje.value);
}

function next(item, length) {
  if (changedPersonaje.value[item] === length) {
    changedPersonaje.value[item] = 1;
  } else {
    changedPersonaje.value[item]++;
  }
  emit("personaje", changedPersonaje.value);
}
</script>

<style lang="scss" scoped>
svg {
  fill: red;
}

.nav {
  display: flex;
  flex-direction: column;
  justify-content: space-around;

  &-block {
    display: flex;
    margin: 10px;
    justify-content: space-evenly;
    align-items: center;
    flex-wrap: nowrap;
  }
}

.icon {
  cursor: pointer;
}
</style>
