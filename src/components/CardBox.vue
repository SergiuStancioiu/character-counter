<script setup lang="ts">
const props = defineProps({
  id: { type: String, required: true },
  name: { type: String, required: true },
  backgroundImage: { type: String, required: true },
  backgroundColor: { type: String, required: true },
  number: { type: Number, required: true },
});

const imageUrl = new URL(
  `../assets/images/${props.backgroundImage}`,
  import.meta.url
).href;
</script>

<template>
  <div
    class="flex items-center justify-between overflow-hidden rounded-xl pl-2.5 max-h-32.5"
    :style="{ backgroundColor }"
  >
    <div class="flex flex-col gap-2.5">
      <h2 class="text-3xl font-medium">{{ props.number }}</h2>
      <p class="text-xl">{{ props.name }}</p>
    </div>
    <div class="-mr-13">
      <img class="w-full" :src="imageUrl" alt="Background Image" />
    </div>
  </div>
</template>
