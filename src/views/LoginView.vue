<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
const router = useRouter();
const username = ref("");
const password = ref("");
const error = ref(false);
const login = () => {
  if (username.value === "tmdb" && password.value === "movies") {
    router.push("/Purchase");
  } else {
    error.value = true;
  }
};
</script>

<template>
  <body>
    <div class="home-container">
      <form @submit.prevent="login()">
        <input type="text" v-model="username" placeholder="Username" />
        <br />
        <input type="password" v-model="password" placeholder="Password" />
        <br />
        <input type="submit" value="Login" />
      </form>
      <div v-if="error" class="error">
        <p>Incorrect!! Try Again!!</p>
      </div>
    </div>
  </body>
</template>

<style scoped>
.home-container {
  display: flex;
  position: absolute;
  top: 300px;
  right: 455px;
  text-align: center;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  align-items: center;
  justify-content: center;
}

body {
  height: 100vh;
  background-position: center;
  background-size: 100%;
  background-image: url("https://img.freepik.com/free-photo/arrangement-movie-elements-blue-background-with-copy-space_23-2148457886.jpg?w=740&t=st=1673487467~exp=1673488067~hmac=72d245e2618a4b80dec953d58e5c289d726473c8afca4da90ddda5b50829bda4");
}
</style>