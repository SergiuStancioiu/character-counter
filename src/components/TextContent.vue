<script setup lang="ts">
import { ref, computed } from 'vue';

import Checkbox from './Checkbox.vue';
import CardBox from './CardBox.vue';

const totalCharacters = ref('');
const excludeSpaces = ref(false);
const setCharacterLimit = ref(false);
const characterLimitNumber = ref(0);

const totalCharactersNumber = computed(() => {
  if (excludeSpaces.value) {
    return totalCharacters.value.replace(/\s+/g, '').length;
  }
  return totalCharacters.value.length;
});

const totalWordCountNumber = computed(() => {
  let wordCount = totalCharacters.value.split(' ').filter(function (n) {
    return n != '';
  }).length;

  return wordCount;
});

const totalSentenceCountNumber = computed(() => {
  const numOfSentences =
    totalCharacters.value.match(/\b\p{L}+[.!?](\s|$)/gu)?.length ?? 0;

  return numOfSentences;
});

const setCharacterLimitNumber = computed(() => {
  return setCharacterLimit.value ? characterLimitNumber.value : 10000;
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
          v-model.trim="totalCharacters"
          class="w-full border-textarea-border-light border-2 bg-textarea-background-light pl-2.5 pt-2.5 h-50 rounded-md"
          name="analyze-text"
          id="analyze-text"
          placeholder="Start typing here...(or paste your text)"
          :maxlength="setCharacterLimitNumber"
        ></textarea>
        <p
          v-if="
            setCharacterLimit &&
            characterLimitNumber > 0 &&
            totalCharacters.length == characterLimitNumber
          "
          class="flex gap-1 items-center text-warning-orange text-sm"
        >
          <img src="../assets/images/icon-info.svg" alt="Info Icon" />Limit
          reached! Your text exceeds {{ characterLimitNumber }} characters.
        </p>
        <div class="flex flex-col gap-2">
          <Checkbox
            id="exclude-spaces"
            label="Exclude Spaces"
            name="exclude-spaces"
            v-model="excludeSpaces"
          />
          <div class="flex gap-2.5 min-h-7">
            <Checkbox
              id="set-character-limit"
              label="Set Character Limit"
              name="set-character-limit"
              v-model="setCharacterLimit"
            />
            <input
              v-if="setCharacterLimit"
              v-model.number="characterLimitNumber"
              class="border-input-border-light border-2 rounded-md pl-2.5 max-w-13.75"
              type="number"
              name="Character Limit"
              id="character-limit"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="dark:text-whit pb-11.25">
      Approx. reading time: &lt;1 minute
    </div>
    <div class="flex flex-col gap-4 mb-8">
      <CardBox
        id="total-characters"
        name="Total Characters"
        backgroundImage="pattern-character-count.svg"
        backgroundColor="#d3a1fa"
        :number="totalCharactersNumber"
      />
      <CardBox
        id="word-count"
        name="Word Count"
        backgroundImage="pattern-word-count.svg"
        backgroundColor="#ff9f00"
        :number="totalWordCountNumber"
      />
      <CardBox
        id="sentence-count"
        name="Sentence Count"
        backgroundImage="pattern-sentence-count.svg"
        backgroundColor="#ff8159"
        :number="totalSentenceCountNumber"
      />
    </div>
  </div>
</template>
