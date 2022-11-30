<template lang="pug">
.container
  .person 
    img.person__item.face(src=`@/assets/persons/face_${Math.floor(Math.random() * 6)+1}.svg`)
    img.person__item.cheeks(src=`@/assets/persons/cheeks_${Math.floor(Math.random() * 3)+1}.svg`)
    img.person__item.eyes(src=`@/assets/persons/eyes_${Math.floor(Math.random() * 6)+1}.svg`)
    img.person__item.rot(src=`@/assets/persons/rot_${Math.floor(Math.random() * 8)+1}.svg`)
</template>

<script setup>
import { computed, toRefs } from "vue";

const array = Math.floor(Math.random() * 2) + 1;
const color = "#" + (((1 << 24) * Math.random()) | 0).toString(16);
const test = computed(() => Math.floor(Math.random() * 2) + 1);

console.log(array, color);
</script>

<style lang="scss" scoped>
svg {
  fill: red;
}

.person {
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
  filter: hue-rotate(180deg) drop-shadow(1px 1px 20px rgb(0 0 0 / 70%))
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
