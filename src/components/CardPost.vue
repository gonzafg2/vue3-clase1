<script setup>
defineProps({
  titlePost: String,
  descriptionPost: String,
  idPost: Number,
});
</script>

<template>
  <div class="card mb-4">
    <div class="card-body">
      <h5 class="card-title">{{ titlePost }}</h5>
      <p class="card-text">
        {{ descriptionPost }}
      </p>
      <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
  </div>
</template>

<style>
.card-title {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.card-text {
  text-overflow: ellipsis;
  height: 6rem;
  white-space: break-spaces;
  overflow: hidden;
}
</style>
