<template lang="pug">
.container
  .personaje 
    img.personaje__item.face(:src="require(`@/assets/personajes/face_${personaje.face}.svg`)")
    img.personaje__item.cheeks(:src="require(`@/assets/personajes/cheeks_${personaje.cheeks}.svg`)")
    img.personaje__item.eyes(:src="require(`@/assets/personajes/eyes_${personaje.eyes}.svg`)")
    img.personaje__item.rot(:src="require(`@/assets/personajes/rot_${personaje.rot}.svg`)")

  .nav
    .prev(data-icon="ei-arrow-left" @click="next(personajeo.eyes--)")
    .eyes(data-icon="ei-eye")
    .next(data-icon="ei-arrow-right" @click="next(personaje.eyes++)")
</template>

<script setup>
import { computed, toRefs, defineProps } from "vue";

const props = defineProps({
  personaje: {
    type: Object,
  },
});

const { personaje } = toRefs(props);
const personajeo = toRefs(personaje);

console.log(personaje, personajeo);

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
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: nowrap;
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
