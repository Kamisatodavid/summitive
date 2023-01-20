<script setup>
import axios from "axios";
import { useStore } from "../store/index.js";

const store = useStore();
const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);

let data = (
  await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
    params: {
      api_key: "64688a2ee40628130c4073aff0308684",
      append_to_response: "videos",
    },
  })
).data;
</script>

<template>
  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <h1>{{ data.title }}</h1>
        <h1>{{ data.release_date }}</h1>
        <img
          :src="`https://image.tmdb.org/t/p/w500${data.poster_path}`"
          alt=""
        />
        <iframe
          :src="`https://www.youtube.com/embed/${
            data.videos.results
              .filter((video) => video.type === 'Trailer')
              .at(0).key
          }`"
        ></iframe>
        <div class="purchaseButton-container">
          <button
            @click="
              store.addToCart(props.id, {
                id: data.id,
                poster: data.poster_path,
                title: data.title,
                date: data.release_date,
              })
            "
          >
            Purchase
          </button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
h1 {
  font-size: 25px;
  text-align: center;
  margin: 5px;
  border-style: double;
  border-width: 1px;
  border-color: aqua;
}

iframe {
  position: absolute;
  bottom: 10px;
  flex-direction: row;
  width: 350px;
  aspect-ratio: 3/2;
}

img {
  aspect-ratio: 2/3;
  width: 200px;
  margin: 20px;
}

.purchaseButton-container {
  position: absolute;
  bottom: 0px;
  right: 0px;
}

.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
}

.modal-outer-container .modal-inner-container {
  background-color: #1f2123;
  color: white;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
}

.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: #1f2123;
  font-weight: bold;
  font-size: 1.25rem;
  color: white;
}
</style>
