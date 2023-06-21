<template>
  <h1>Hola {{ name }}</h1>
  <h2 :style="colorGreen">Soy verde</h2>
  <h3 v-if="activo">Estado Activo</h3>
  <ul>
    <li v-for="(fruta, index) in frutas" :key="index">
      {{ index }} - {{ fruta }}
    </li>
  </ul>
</template>

<script setup>
const name = "Vue 3";
const colorGreen = "color: green"
const activo = true
const frutas = ["manzana", "pera", "plátano", "frutilla"]
</script>

<style>
h1 {
  color: red;
}
</style>