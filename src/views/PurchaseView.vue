<script setup>
import { ref } from "vue";
import SiteModal from "../components/SiteModal.vue";
import { useStore } from "../store/index.js";

const store = useStore();
const genre = ref(28);
const showModal = ref(false);
const selectedId = ref(0);

const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};

const closeModal = () => {
  showModal.value = false;
};

const getGenres = async () => {
  await store.getMovies(genre.value);
};
</script>

<template>
  <div class="purchase-container">
    <select v-model="genre" @change="getGenres()">
      <option value="16">Animation</option>
      <option value="28">Action</option>
      <option value="878">Science Fiction</option>
      <option value="12">Adventure</option>
      <option value="9684">Mystery</option>
    </select>
    <h1>Select a movies category you like</h1>
    <RouterLink to="/cart" custom v-slot="{ navigate }">
      <button @click="navigate" role="link">Cart</button>
    </RouterLink>
    <div class="poster-container">
      <img
        v-for="movie in store.movies"
        :id="movie.id"
        @click="openModal(movie.id)"
        :src="`https://image.tmdb.org/t/p/w500${movie.poster}`"
      />
      <SiteModal
        v-if="showModal"
        @toggleModal="closeModal()"
        :id="selectedId"
      />
    </div>
  </div>
</template>

<style scoped>
.poster-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
}

h1 {
  color: aliceblue;
}

img {
  margin: 10px;
  aspect-ratio: 2/3;
  width: 230px;
  border-style: double;
  border-width: 1px;
  border-color: aqua;
}

.purchase-container {
  background-color: black;
}

button {
  position: absolute;
  top: 1px;
  right: 1px;
  color: darkred;
  border-style: double;
  border-width: 4px;
  border-color: rgb(255, 0, 0);
}
</style>