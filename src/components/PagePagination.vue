<template>
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
        <li class="page-item" v-for="(page, i) in getPagesPagination" :key="i">
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
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  data: Array,
});

const emit = defineEmits(["changePage"]);

const pageActual = ref(1);

const getPagesPagination = computed(() => Math.ceil(props.data?.length / 12));

const pageInitialDisabled = computed(() =>
  pageActual.value === 1 ? "disabled" : ""
);

const pageFinalDisabled = computed(() =>
  pageActual.value === getPagesPagination.value ? "disabled" : ""
);

const setPageActual = (page) => {
  pageActual.value = page;
  emit("changePage", pageActual.value);
};

const setPreviousPage = () => {
  pageActual.value > 1 ? pageActual.value-- : 0;
  emit("changePage", pageActual.value);
};

const setNextPage = () => {
  pageActual.value !== getPagesPagination ? pageActual.value++ : 0;
  emit("changePage", pageActual.value);
};
</script>
