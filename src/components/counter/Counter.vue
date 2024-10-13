<script setup lang="ts">
import Button from "../button/Button.vue";

import { reactive } from "vue";
import { ref } from "vue";

const counterProps = defineProps<{
  title: string;
  initialValue: number;
  min: number;
  max: number;
  step: number;
}>();

const isAnimated = ref<boolean>(false);

const counterStore = reactive({
  value: counterProps.initialValue,
  triggerAnimation(): void {
    isAnimated.value = true;

    setTimeout(() => {
      isAnimated.value = false;
    }, 500);
  },
  increment(): void {
    this.value = Math.min(this.value + counterProps.step, counterProps.max);
    this.triggerAnimation();
  },
  decrement(): void {
    this.value = Math.max(this.value - counterProps.step, counterProps.min);
    this.triggerAnimation();
  },
  resetPrompt(): boolean {
    return window.confirm("Вы точно уверены");
  },
  resetValue(): void {
    this.value = counterProps.initialValue;
  },
  reset(): void {
    this.resetPrompt() && this.resetValue();
    this.triggerAnimation();
  },
  init(): void {
    this.value = Number(prompt("Введите число"));
  },
  getColor(): string {
    return this.value < counterProps.initialValue ? "blue" : this.value === counterProps.initialValue ? "black" : "green";
  },
});
</script>

<template>
  <div class="counter">
    <h2 class="counter__title">{{ counterProps.title }}</h2>
    <span
      :class="['counter__value', { 'counter--animate': isAnimated }]"
      :style="{ color: counterStore.getColor() }"
      @click="() => counterStore.init()"
      >{{ counterStore.value }}</span
    >

    <div class="counter__controllers">
      <Button title="-" :clickHanlder="() => counterStore.decrement()" />
      <Button title="Сбросить" :clickHanlder="() => counterStore.reset()" />
      <Button title="+" :clickHanlder="() => counterStore.increment()" />
    </div>
  </div>
</template>

<style scoped>
.counter {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  padding: 30px;
  border-radius: 20px;
  box-shadow: 4px 4px 14px 12px rgba(34, 60, 80, 0.2);
}

.counter__title {
  margin: 0;
  margin-bottom: 10px;
}

.counter__value {
  margin-bottom: 20px;
  font-size: 30px;
}

.counter__controllers {
  display: flex;
  gap: 5px;
}

.counter--animate {
  animation: scaleAnim 0.5s ease-in-out;
}

@keyframes scaleAnim {
  from {
    transform: scale(0.85);
  }
  50% {
    transform: scale(1.5);
  }
  to {
    transform: scale(0.85);
  }
}
</style>
