<template lang="pug">
.personaje 
  img.personaje__item.face(:src="require(`@/assets/personajes/face_${personaje.face}.svg`)")
  img.personaje__item.cheeks(:src="require(`@/assets/personajes/cheeks_${personaje.cheeks}.svg`)")
  img.personaje__item.eyes(:src="require(`@/assets/personajes/eyes_${personaje.eyes}.svg`)")
  img.personaje__item.rot(:src="require(`@/assets/personajes/rot_${personaje.rot}.svg`)")

</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  personaje: {
    type: Object,
  },
});
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
