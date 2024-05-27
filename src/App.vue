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
import { onMounted, ref, createApp, nextTick } from 'vue';
import MicroApp from "@/components/MicroApp.vue";

const shadowHost = ref<HTMLElement | null>(null);

const fetchStyleContent = async (href: string): Promise<string> => {
  const response = await fetch(href);
  if (!response.ok) {
    throw new Error(`Error fetching stylesheet ${href}: ${response.statusText}`);
  }
  return response.text();
};

const appendGlobalStyles = (styleElement: HTMLStyleElement): void => {
  const globalStyles = document.querySelectorAll<HTMLStyleElement>('style');
  globalStyles.forEach(style => {
    if (style.innerHTML) {
      styleElement.textContent += style.innerHTML;
    }
  });
};

const appendLinkStyles = async (styleElement: HTMLStyleElement): Promise<void> => {
  const globalLinks = document.querySelectorAll<HTMLLinkElement>('link[rel="stylesheet"]');
  for (const link of globalLinks) {
    try {
      const styleContent = await fetchStyleContent(link.href);
      styleElement.textContent += styleContent;
    } catch (error) {
      console.error(error.message);
    }
  }
};

const copyStylesToShadowRoot = async (shadowRoot: ShadowRoot): Promise<void> => {
  const styleElement = document.createElement('style');
  await appendLinkStyles(styleElement);
  appendGlobalStyles(styleElement);
  shadowRoot.appendChild(styleElement);
};

const initializeShadowRoot = () => {
  if (!shadowHost.value) return;

  const shadowRoot = shadowHost.value.attachShadow({ mode: 'open' });
  const appInstance = createApp(MicroApp);
  appInstance.mount(shadowRoot);

  nextTick(() => copyStylesToShadowRoot(shadowRoot));
};

onMounted(() => {
  initializeShadowRoot();
});
</script>


<style scoped>


</style>
