<template>
  <div id="micro-app">
    <ImageGallery :imagesData="imagesData"/>
    <div id="photoswiper" />
    <div class="listStyle">
      <button @click="pushItem">add</button>
      <TransitionGroup name="list"
                       tag="ul"
      >
        <li v-for="(item, index) in items"
            :key="index"
            :data-index="index"
        >
          {{ item }}
        </li>
      </TransitionGroup>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
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

const items = ref([]);

const pushItem = () => {
  items.value.push(Math.floor(Math.random() * 10));
};
</script>

<style scoped>
.listStyle {
  li {
    background-color: #8a8997;
    margin: 4px;
    font-size: 14px;
  }
}

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
