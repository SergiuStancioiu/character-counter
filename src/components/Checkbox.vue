<script setup lang="ts">
const props = defineProps({
  id: { type: String, required: true },
  label: { type: String, required: true },
  name: { type: String, required: true },
  modelValue: { type: Boolean, required: true },
});

const emit = defineEmits(['update:modelValue']);

const onChange = (event: Event) => {
  const target = event.target as HTMLInputElement;
  emit('update:modelValue', target.checked);
};
</script>

<template>
  <div class="flex items-center gap-1.5 justify-start">
    <input
      type="checkbox"
      :name="props.name"
      :id="props.id"
      :checked="modelValue"
      @change="onChange"
    />
    <label class="dark:text-white" :for="props.id">{{ props.label }}</label>
  </div>
</template>
