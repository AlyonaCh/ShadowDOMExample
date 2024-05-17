<template>
  <header>
    <div class="wrapper"></div>
  </header>

  <main>
    <div>
      <h2>Shadow element:</h2>
      <div ref="shadowHost"></div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref, createApp } from 'vue';
import MicroApp from "@/components/MicroApp.vue";

const shadowHost = ref<HTMLElement | null>(null);

const createAndAppendStyleElement = (shadowRoot: ShadowRoot) => {
  const styleElement = document.createElement('style');
  shadowRoot.prepend(styleElement);
  return styleElement;
};

const copyStylesToShadowRoot = (styleElement: HTMLStyleElement) => {
  const globalStyles = document.querySelectorAll('style');
  globalStyles.forEach(style => {
    if (style.innerHTML) {
      styleElement.append(style.innerHTML);
    }
  });
};

const initializeShadowRoot = () => {
  if (!shadowHost.value) return;

  const shadowRoot = shadowHost.value.attachShadow({ mode: 'open' });
  const appInstance = createApp(MicroApp);
  appInstance.mount(shadowRoot);

  const styleElement = createAndAppendStyleElement(shadowRoot);
  copyStylesToShadowRoot(styleElement);
};

onMounted(() => {
  initializeShadowRoot();
});
</script>


<style scoped>


</style>
