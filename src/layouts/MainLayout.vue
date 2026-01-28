<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import FlowHeader from "components/FlowHeader.vue";
import FlowQuickMenu from "components/FlowQuickMenu.vue";
import MainPage from "src/pages/MainPage.vue";

const headerRef = ref(null);
const pageHeight = ref(null);

onMounted(() => {
  adjustPageHeight();
  window.addEventListener("resize", adjustPageHeight);
});

onUnmounted(() => {
  window.removeEventListener("resize", adjustPageHeight);
});

function adjustPageHeight() {
  pageHeight.value = window.innerHeight - headerRef.value.$el.offsetHeight;
}
</script>

<template>
  <q-layout view="hHh LpR lFf" class="min-width-layout">
    <FlowHeader ref="headerRef" />

    <FlowQuickMenu />

    <q-page-container ref="pageContainerRef">
      <main-page :style="{ height: pageHeight + 'px' }" />
    </q-page-container>

  </q-layout>
</template>

<style lang="scss" scoped>
.min-width-layout {
  min-width: $body-width;
}
</style>
