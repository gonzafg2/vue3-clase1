<template>
  <button class="btn btn-primary" @click="emitColor('changeColorTextEmits', changeColorText)">Cambiar color</button>
</template>

<script setup>
import { ref, computed } from "vue";
const colors = ["blue", "red", "green", "yellow", "pink", "purple", "orange"];

const active = ref(false);

const emitColor = defineEmits(["changeColorTextEmits"]);

const changeActive = () => (active.value = !active.value);

const changeColorText = computed(() => {
  changeActive();
  const random = Math.random() * colors.length * active.value;
  return "color:" + colors[Math.round(random)];
});
</script>
