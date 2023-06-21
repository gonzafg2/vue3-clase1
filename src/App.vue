<template>
  <h1 :style="changeColorText">Hola {{ name }}</h1>
  <button @click="changeActive">Cambiar color</button>
  {{ active }}
</template>

<script setup>
import { ref, computed } from 'vue'

const name = "Vue 3";
const colors = ['blue', 'red', 'green', 'yellow', 'pink', 'purple', 'orange']

let active = ref(false);

const changeActive = () => (active.value = !active.value)

const changeColorText = computed(() => {
  const random = Math.random() * colors.length * active.value
  console.log(random, Math.round(random));
  return 'color:' + colors[Math.round(random)]
});
</script>

<style></style>
