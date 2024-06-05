<script setup>
import TextGenerator from './components/TextGenerator.vue'
import ImageGenerator from './components/ImageGenerator.vue'
</script>

<template>
  <div class="root">
    <TextGenerator />
    <ImageGenerator />
  </div>
</template>

<style scoped>
.root {
  position: relative;
}
</style>
