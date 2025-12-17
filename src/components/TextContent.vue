<script setup lang="ts">
import Checkbox from './Checkbox.vue';
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
          class="w-full border border-gray-200 bg-gray-100 pl-2.5 pt-2.5 h-50 rounded-md"
          name="analyze-text"
          id="analyze-text"
          placeholder="Start typing here...(or paste your text)"
        ></textarea>
        <div>
          <Checkbox
            id="exclude-spaces"
            label="Exclude Spaces"
            name="exclude-spaces"
          />
          <Checkbox
            id="set-character-limit"
            label="Set Character Limit"
            name="set-character-limit"
          />
        </div>
      </div>
    </div>
    <div class="dark:text-white">Approx. reading time: &lt;1 minute</div>
  </div>
</template>
