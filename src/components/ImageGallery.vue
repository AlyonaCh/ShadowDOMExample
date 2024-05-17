<template>
  <div class="gallery">
    <button @click="openGallery">Open gallery</button>
<!--    <Teleport v-if="isMounted" to="#photoswiper">-->
      <div ref="containerPhotoswiper" />
<!--    </Teleport>-->
  </div>
</template>

<script setup lang="ts">
import {
  onMounted, onUnmounted, Ref, ref
} from 'vue';
import PhotoSwipeLightbox from 'photoswipe/lightbox';


const isMounted = ref(false);

onMounted(() => {
  isMounted.value = true;
});

const containerPhotoswiper = ref(null);

const lightbox: Ref<PhotoSwipeLightbox | null> = ref(null);

const props = defineProps({
  imagesData: {
    type: Array,
    required: true,
  }
});

const openGallery = async () => {
  lightbox.value?.loadAndOpen(0);
};

const openGalleryIndex = async (index: number) => {
  lightbox.value?.loadAndOpen(index);
};

onMounted(async () => {
  if (!lightbox.value) {
    const appendElement = containerPhotoswiper.value;
    lightbox.value = new PhotoSwipeLightbox({
      pswpModule: () => import('photoswipe'),
      dataSource: props.imagesData,
      mainClass: 'pswp pswp-custom',
      secondaryZoomLevel: 2,
      maxZoomLevel: 3,
      zoom: true,
      appendToEl: appendElement,
    });
    lightbox.value.init();
  }
});

onUnmounted(() => {
  if (lightbox.value) {
    lightbox.value.destroy();
    lightbox.value = null;
  }
});
</script>
<style>
@import 'photoswipe/style.css';
.gallery {
  width: 300px;
  height: auto;
}
</style>
