<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HomeHero from "./components/HomeHero.vue";
import BlogPosts from "./components/BlogPosts.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <div>
    <main class="container">
      <HomeHero title="Blog Posts" />
      <BlogPosts />
      <!-- <RouterView /> -->
    </main>
    <Footer />
  </div>
</template>
