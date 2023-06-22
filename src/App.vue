<template>
  <div class="container">
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
    <div class="row">
      <nav aria-label="Pagination posts from JSONPlaceholder">
        <ul class="pagination justify-content-center">
          <li
            class="page-item"
            :class="pageInitialDisabled"
            @click="setPreviousPage"
          >
            <a class="page-link" href="#">Previo</a>
          </li>
          <li
            class="page-item"
            v-for="(page, i) in getPagesPagination"
            :key="i"
          >
            <a
              class="page-link"
              :class="page === pageActual ? 'active' : ''"
              href="#"
              @click="setPageActual(page)"
              >{{ page }}</a
            >
          </li>
          <li class="page-item" :class="pageFinalDisabled" @click="setNextPage">
            <a class="page-link" href="#">Siguiente</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

import TitlePage from "./components/TitlePage.vue";
import ButtonChangeColor from "./components/ButtonChangeColor.vue";
import CardPost from "./components/CardPost.vue";

const color = ref("color: black");
const postsAPI = ref([]);
const pageActual = ref(1);

const changeColorText = (colorEmits) => (color.value = colorEmits);

const getPosts = (async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await response.json();
  postsAPI.value = data;
})();

const getPagesPagination = computed(() =>
  Math.ceil(postsAPI.value?.length / 12)
);

const pageInitialDisabled = computed(() =>
  pageActual.value === 1 ? "disabled" : ""
);

const pageFinalDisabled = computed(() =>
  pageActual.value === getPagesPagination ? "disabled" : ""
);

const setPageActual = (page) => (pageActual.value = page);

const setPreviousPage = () => (pageActual.value > 1 ? pageActual.value-- : 0);

const setNextPage = () =>
  pageActual.value !== getPagesPagination ? pageActual.value++ : 0;

const postsPagination = computed(() => {
  const start = (pageActual.value - 1) * 12;
  const end = start + 12;
  return postsAPI.value.slice(start, end);
});
</script>
