<template lang="pug">
.container
  .personaje 
    img.personaje__item.face(:src="require(`@/assets/personajes/face_${changedPersonaje.face}.svg`)")
    img.personaje__item.cheeks(:src="require(`@/assets/personajes/cheeks_${changedPersonaje.cheeks}.svg`)")
    img.personaje__item.eyes(:src="require(`@/assets/personajes/eyes_${changedPersonaje.eyes}.svg`)")
    img.personaje__item.rot(:src="require(`@/assets/personajes/rot_${changedPersonaje.rot}.svg`)")

  .nav
    .prev(data-icon="ei-arrow-left" @click="changedPersonaje.eyes = 5")
    .eyes(data-icon="ei-eye")
    .nav-next(data-icon="ei-arrow-right" @click="test")
</template>

<script setup>
import { computed, ref, toRefs, defineProps } from "vue";

const props = defineProps({
  personaje: {
    type: Object,
  },
});

const { personaje } = toRefs(props);
let changedPersonaje = ref({
  face: personaje.value.split(", ")[0],
  cheeks: personaje.value.split(", ")[1],
  eyes: personaje.value.split(", ").map(Number)[2],
  rot: personaje.value.split(", ")[3],
});

function test() {
  console.log(changedPersonaje.value);
  changedPersonaje.value.eyes = 1;
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
    left: 50%;
    transform: translateX(-50%);
  }
}

.nav {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: nowrap;

  &-next {
    cursor: pointer;
    background: red;
  }
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
