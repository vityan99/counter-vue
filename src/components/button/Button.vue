<script setup lang="ts">
defineProps<{
  title: string;
  clickHanlder: () => void;
}>();
</script>

<template>
  <button class="btn" @click="clickHanlder">{{ title }}</button>
</template>

<style scoped>
.btn {
  background-color: transparent;
  border: none;
  padding: 10px 22px;
  outline: 1px solid #a7a7a7;
  border-radius: 8px;
  cursor: pointer;
}
</style>
