<template>
  <div class="font-poppins">
    <NuxtPage />
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(async () => {
  // Import AOS dynamically on the client side
  if (process.client) {
    const AOS = await import('aos');
    await import('aos/dist/aos.css');
    AOS.default.init({
      offset: 0,
      duration: 1000
    });
  }
});
</script>

<style>
html {
  scroll-behavior: smooth;
}
</style>