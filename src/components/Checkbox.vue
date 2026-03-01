<script setup lang="ts">
export type CheckboxProps = {
  id: string;
  label: string;
  name: string;
  modelValue: boolean;
};

const props = defineProps<CheckboxProps>();

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
