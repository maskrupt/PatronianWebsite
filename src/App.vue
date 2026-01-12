<script setup>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="flex flex-col min-h-screen">
    <Navbar />
    <main class="grow">
      <router-view />
    </main>
    <Footer />
  </div>
</template>

<style>
/* Global styles are in style.css */
</style>
