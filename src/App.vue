<template>
  <LoadingPage v-if="loading" />
  <div class="container" v-else>
    <div class="row text-center mt-3 mb-4">
      <div class="col-12">
        <TitlePage :colorClass="color" />
      </div>
      <div class="col-12">
        <ButtonChangeColor @changeColorTextEmits="changeColorText" />
      </div>
    </div>
    <div class="row">
      <div v-for="post in postsPagination" class="col-4">
        <CardPost
          :titlePost="post.title"
          :descriptionPost="post.body"
          :idPost="post.id"
        />
      </div>
    </div>
    <PagePagination :data="postsAPI" @changePage="changePage"></PagePagination>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

import TitlePage from "./components/TitlePage.vue";
import ButtonChangeColor from "./components/ButtonChangeColor.vue";
import CardPost from "./components/CardPost.vue";
import PagePagination from "./components/PagePagination.vue";
import LoadingPage from "./components/LoadingPage.vue";

const color = ref("color: black");
const postsAPI = ref([]);
const pageActual = ref(1);
const loading = ref(true);

const changeColorText = (colorEmits) => (color.value = colorEmits);

const getPosts = (async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    const data = await response.json();
    postsAPI.value = data;
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
})();

const postsPagination = computed(() => {
  const start = (pageActual.value - 1) * 12;
  const end = start + 12;
  return postsAPI.value.slice(start, end);
});

const changePage = (page) => (pageActual.value = page);
</script>
