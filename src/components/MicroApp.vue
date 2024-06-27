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
    src: "https://placehold.co/800x600/EEE/31343C",
    largeURL: "https://placehold.co/1600x1200/EEE/31343C",
    width: 800,
    height: 600
  },
  {
    src: "https://placehold.co/800x600/EEE/FFF0F5",
    largeURL: "https://placehold.co/1600x1200/EEE/FFF0F5",
    width: 800,
    height: 600
  },
  {
    src: "https://placehold.co/800x600/EEE/87CEFA",
    largeURL: "https://placehold.co/1600x1200/EEE/87CEFA",
    width: 800,
    height: 600
  },
];
</script>

<style scoped>

</style>
