<script setup></script>

<template>
  <div class="d-flex flex-column h-vh-100 justify-content-center align-items-center">
    <div class="spinner-border text-primary spinner" role="status">
      <span class="visually-hidden">Cargando...</span>
    </div>
    <p class="text-center mt-3">Cargando...</p>
  </div>
</template>

<style>
.h-vh-100 {
  height: 100vh;
}
.spinner {
  width: 3rem;
  height: 3rem;
}
</style>
