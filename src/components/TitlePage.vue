<template>
  <h1 :style="colorClass">Hola {{ name }}</h1>
</template>

<script setup>
const name = "Vue 3";

defineProps({
  colorClass: {
    type: String,
    default: "color: black",
  },
});
</script>
