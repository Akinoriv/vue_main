<template lang="pug">
.container
  Person(:personaje="changedPersonaje")
  //- .personaje 
    img.personaje__item.face(:src="require(`@/assets/personajes/face_${changedPersonaje.face}.svg`)")
    img.personaje__item.cheeks(:src="require(`@/assets/personajes/cheeks_${changedPersonaje.cheeks}.svg`)")
    img.personaje__item.eyes(:src="require(`@/assets/personajes/eyes_${changedPersonaje.eyes}.svg`)")
    img.personaje__item.rot(:src="require(`@/assets/personajes/rot_${changedPersonaje.rot}.svg`)")

  // TODO: add v-for for changedPersonaje
  .nav
    .nav-block
      font-awesome-icon.icon.icon-prev(icon="arrow-left" @click="prev('eyes', 11)")
      font-awesome-icon.icon.icon-center(icon="eye")
      font-awesome-icon.icon.icon-next(icon="arrow-right" @click="next('eyes', 11)")
    .nav-block
      font-awesome-icon.icon.icon-prev(icon="arrow-left" @click="prev('rot', 12)")
      font-awesome-icon.icon.icon-center(icon="meh-blank")
      font-awesome-icon.icon.icon-next(icon="arrow-right" @click="next('rot', 12)")
</template>

<script setup>
import Person from "./Person.vue";
import { computed, ref, toRefs, defineProps, defineEmits } from "vue";

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
  personajeParser(personaje.value);
}

// TODO: save length of imgs for personajes
function personajeParser(personaje) {
  console.log("personaje", personaje);
  changedPersonaje.value = JSON.parse(personaje.value);
  // changedPersonaje.value = {
  //   face: personaje.split(", ")[0],
  //   cheeks: personaje.split(", ")[1],
  //   eyes: personaje.split(", ")[2],
  //   rot: personaje.split(", ")[3],
  // };

  // $emit("update:modelValue", changedPersonaje.value);
  // emit("personaje", changedPersonaje.value);
}

function prev(item, length) {
  if (changedPersonaje.value[item] === 1) {
    changedPersonaje.value[item] = length;
  } else {
    changedPersonaje.value[item]--;
  }
}

function next(item, length) {
  if (changedPersonaje.value[item] === length) {
    changedPersonaje.value[item] = 1;
  } else {
    changedPersonaje.value[item]++;
  }
}

const color = "#" + (((1 << 24) * Math.random()) | 0).toString(16);
</script>

<style lang="scss" scoped>
svg {
  fill: red;
}

.personaje {
  position: relative;
  width: 100px;
  height: 100px;
  margin: 0 auto;
  padding: 0;

  &__item {
    position: absolute;
    user-select: none;
    left: 50%;
    transform: translateX(-50%);
  }
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
.face {
  filter: hue-rotate(180deg) drop-shadow(1px 1px 5px rgb(0 0 0 / 70%))
    brightness(1.5);
  width: 100%;
}
.cheeks {
  width: 70%;
  top: 45%;
}
.eyes {
  width: 70%;
  bottom: 50%;
  filter: drop-shadow(1px 2px 2px black);
}
.rot {
  width: 20%;
  max-height: 20%;
  top: 60%;
}

.filter-green {
  filter: invert(48%) sepia(79%) saturate(2476%) hue-rotate(86deg)
    brightness(118%) contrast(119%);
}

#face {
  fill: green;
}
</style>
