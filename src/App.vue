<template>
  <h1 :style="changeColorText">Hola {{ name }}</h1>
  <button class="btn btn-primary" @click="changeActive">Cambiar color</button>
</template>

<script setup>
import { ref, computed } from 'vue'

const name = "Vue 3";
const colors = ['blue', 'red', 'green', 'yellow', 'pink', 'purple', 'orange']

let active = ref(false);

const changeActive = () => (active.value = !active.value)

const changeColorText = computed(() => {
  const random = Math.random() * colors.length * active.value
  return 'color:' + colors[Math.round(random)]
});
</script>

<style></style>
