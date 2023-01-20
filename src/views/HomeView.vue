<script setup>
import SiteHeader from "../components/SiteHeader.vue";
import SiteFooter from "../components/SiteFooter.vue";
import SiteHero from "../components/SiteHero.vue";
</script>

<template>
  <div class="component-container">
    <SiteHeader />
    <SiteHero />
    <SiteFooter />
  </div>
</template>

<style scoped>
.component-container {
  height: 100vh;
  background-position: center;
  background-size: 100%;
  background-image: url("https://img.freepik.com/free-vector/clapper-board-design-black-background_1017-38726.jpg?w=826&t=st=1673489820~exp=1673490420~hmac=ca9c4be532a1a9c0f0a28390f790b20cbf6a735d685c1a67ac8db4e0ad7a3dc5");
}
</style>