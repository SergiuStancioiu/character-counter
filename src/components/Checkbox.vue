<script setup lang="ts">
const props = defineProps({
  id: { type: String, required: true },
  label: { type: String, required: true },
  name: { type: String, required: true },
});
</script>

<template>
  <div class="flex items-center gap-1.5 justify-start">
    <input type="checkbox" :name="props.name" :id="props.id" />
    <label class="dark:text-white" :for="props.id">{{ props.label }}</label>
  </div>
</template>
