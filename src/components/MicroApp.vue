<template>
  <div id="micro-app">
    <ImageGallery :imagesData="imagesData"/>
    <div id="photoswiper" />
  </div>
</template>

<script setup lang="ts">
import ImageGallery from "@/components/ImageGallery.vue";

const imagesData = [
  {
    src: "https://source.unsplash.com/random/800x600",
    largeURL: "https://source.unsplash.com/random/1600x1200",
    width: 800,
    height: 600
  },
  {
    src: "https://source.unsplash.com/random/800x600",
    largeURL: "https://source.unsplash.com/random/1600x1200",
    width: 800,
    height: 600
  },
  {
    src: "https://source.unsplash.com/random/800x600",
    largeURL: "https://source.unsplash.com/random/1600x1200",
    width: 800,
    height: 600
  },
  {
    src: "https://source.unsplash.com/random/800x600",
    largeURL: "https://source.unsplash.com/random/1600x1200",
    width: 800,
    height: 600
  },
];
</script>

<style scoped>

</style>
