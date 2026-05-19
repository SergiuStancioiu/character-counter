<script setup lang="ts">
import { computed, ref } from 'vue';
import RangeBar from './RangeBar.vue';

export type LetterDensityProps = {
  text: string;
};

const props = defineProps<LetterDensityProps>();

const showAll = ref(false);

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

const visibleLetterCounts = computed(() => {
  return showAll.value ? letterCounts.value : letterCounts.value.slice(0, 5);
});
</script>

<template>
  <div class="flex flex-col gap-4">
    <div class="text-2xl text-black dark:text-white font-medium">
      Letter Density
    </div>

    <div v-if="letterCounts.length > 0">
      <div v-for="[char, count] in visibleLetterCounts" :key="char">
        <RangeBar :label="char" :value="count" />
      </div>

      <!-- See more / See less button -->
      <button
        v-if="letterCounts.length > 5"
        @click="showAll = !showAll"
        class="mt-3 text-blue-500 hover:underline"
      >
        {{ showAll ? 'See less' : 'See more' }}
      </button>
    </div>

    <div v-else class="dark:text-white">
      No characters found. Start typing to see letter density.
    </div>
  </div>
</template>
