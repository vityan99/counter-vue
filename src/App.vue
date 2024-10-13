<script setup lang="ts">
import Counter from "./components/counter/Counter.vue";
</script>

<template>
  <div class="container">
    <Counter title="Счётчик" :initialValue="0" :min="-10" :max="10" :step="5" />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>
