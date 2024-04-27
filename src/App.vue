<template>
  <header>

    <div class="wrapper">
    </div>
  </header>

  <main>
    <div>
      <h2>Shadow element:</h2>
      <div ref="elRoot" />
    </div>
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref, createApp } from 'vue';
import MicroApp from "@/components/MicroApp.vue";

const elRoot = ref(null);
let elementMountApp = null;
const setupShadowRoot = () => {
  if (!elRoot.value) return;
  const shadowRoot = elRoot.value.attachShadow({ mode: 'open' });
  const component = createApp(MicroApp);
  component.mount(shadowRoot);
};

onMounted(() => {
  setupShadowRoot();
});


</script>


<style scoped>


</style>
