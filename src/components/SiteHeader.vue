<script setup>
</script>

<template>
  <div class="button-container">
    <RouterLink to="/login" custom v-slot="{ navigate }">
      <button @click="navigate" role="link">Login</button>
    </RouterLink>
  </div>
  <div class="header-container">
    <h1>It's time to ENJOY some movies</h1>
  </div>
</template>

<style scoped>
h1 {
  color: aliceblue;
  margin: 30px;
}

.button-container {
  text-align: end;
}
</style>
