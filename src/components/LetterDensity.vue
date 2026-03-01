<script setup lang="ts">
import { computed } from 'vue';
import RangeBar from './RangeBar.vue';

export type LetterDensityProps = {
  text: string;
};

const props = defineProps<LetterDensityProps>();
const letterCounts = computed<Array<[string, number]>>(() => {
  const counts = new Map<string, number>();

  for (const char of props.text.toLowerCase()) {
    if (char !== ' ') {
      counts.set(char, (counts.get(char) ?? 0) + 1);
    }
  }

  return [...counts.entries()].sort((a, b) => {
    // sort by count DESC
    if (b[1] !== a[1]) {
      return b[1] - a[1];
    }

    // if equal, sort alphabetically ASC
    return a[0].localeCompare(b[0]);
  });
});
</script>
<template>
  <div class="flex flex-col gap-4">
    <div class="text-2xl text-black font-medium">Letter Density</div>
    <div>
      <div v-for="[char, count] in letterCounts" :key="char">
        <RangeBar :label="char" :value="count" />
      </div>
    </div>
  </div>
</template>
