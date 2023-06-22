<template>
  <TitlePage :colorClass="color" />
  <ButtonChangeColor @changeColorTextEmits="changeColorText" />
</template>

<script setup>
import { ref } from "vue";

import TitlePage from "./components/TitlePage.vue";
import ButtonChangeColor from "./components/ButtonChangeColor.vue";

const color = ref("color: black");

const changeColorText = (colorEmits) => (color.value = colorEmits);
</script>
