<script setup lang="ts">
import { ref, computed } from 'vue';

import Checkbox from './Checkbox.vue';
import CardBox from './CardBox.vue';

const cardBoxArr = [
  {
    id: 'total-characters',
    name: 'Total Characters',
    backgroundImage: 'pattern-character-count.svg',
    backgroundColor: '#d3a1fa',
  },
  {
    id: 'word-count',
    name: 'Word Count',
    backgroundImage: 'pattern-word-count.svg',
    backgroundColor: '#ff9f00',
  },
  {
    id: 'sentence-count',
    name: 'Sentence Count',
    backgroundImage: 'pattern-sentence-count.svg',
    backgroundColor: '#ff8159',
  },
];

const totalCharacters = ref('');
const excludeSpaces = ref(false);
const setCharacterLimit = ref(false);

const totalCharactersNumber = computed(() => {
  if (excludeSpaces.value) {
    return totalCharacters.value.replace(/\s+/g, '').length;
  }
  return totalCharacters.value.length;
});
</script>

<template>
  <div class="px-4">
    <div class="flex flex-col gap-10">
      <h1
        class="text-black text-4xl pt-10 text-center font-bold dark:text-white"
      >
        Analyze your text in real-time
      </h1>
      <div>
        <textarea
          v-model="totalCharacters"
          class="w-full border-textarea-border-light border-2 bg-textarea-background-light pl-2.5 pt-2.5 h-50 rounded-md"
          name="analyze-text"
          id="analyze-text"
          placeholder="Start typing here...(or paste your text)"
        ></textarea>
        <div>
          <Checkbox
            id="exclude-spaces"
            label="Exclude Spaces"
            name="exclude-spaces"
            v-model="excludeSpaces"
          />
          <Checkbox
            id="set-character-limit"
            label="Set Character Limit"
            name="set-character-limit"
            v-model="setCharacterLimit"
          />
        </div>
      </div>
    </div>
    <div class="dark:text-whit pb-11.25">
      Approx. reading time: &lt;1 minute
    </div>
    <div class="flex flex-col gap-4 mb-8">
      <div v-for="cardBox in cardBoxArr" :key="cardBox.id">
        <CardBox
          :id="cardBox.id"
          :name="cardBox.name"
          :backgroundImage="cardBox.backgroundImage"
          :backgroundColor="cardBox.backgroundColor"
          :number="totalCharactersNumber"
        />
      </div>
    </div>
  </div>
</template>
