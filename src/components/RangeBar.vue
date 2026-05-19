<template>
  <div class="range-bar dark:text-white">
    <div class="uppercase">{{ label }}</div>
    <div class="range-bar-track">
      <div
        class="range-bar-fill"
        :style="{ width: normalizedValue + '%' }"
      ></div>
    </div>

    <span class="range-bar-value dark:text-white">
      {{ normalizedValue }}%
    </span>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  value: {
    type: Number,
    required: true,
    default: 0,
  },
  label: {
    type: String,
    required: true,
  },
});

/* Ensure value always stays between 0 and 100 */
const normalizedValue = computed(() => {
  return Math.min(100, Math.max(0, Math.round(props.value)));
});
</script>

<style scoped>
.range-bar {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: sans-serif;
}

.range-bar-track {
  flex: 1;
  height: 12px;
  background: #e5e7eb;
  border-radius: 999px;
  overflow: hidden;
}

.range-bar-fill {
  height: 100%;
  background: #c084fc; /* purple-400 */
  transition: width 0.3s ease;
}

.range-bar-value {
  min-width: 40px;
  text-align: right;
  font-size: 14px;
}
</style>
