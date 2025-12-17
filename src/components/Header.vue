<script setup lang="ts">
import { ref, onMounted } from 'vue';

const isDark = ref(false);

const applyTheme = (value: boolean) => {
  document.documentElement.classList.toggle('dark', value);
  localStorage.theme = value ? 'dark' : 'light';
};

onMounted(() => {
  const systemDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

  isDark.value =
    localStorage.theme === 'dark' || (!localStorage.theme && systemDark);

  applyTheme(isDark.value);
});

const toggleTheme = () => {
  isDark.value = !isDark.value;
  applyTheme(isDark.value);
};
</script>

<template>
  <header class="p-4 flex items-center justify-between">
    <img
      v-if="!isDark"
      src="../assets/images/logo-light-theme.svg"
      alt="Logo Light"
    />
    <img
      v-if="isDark"
      src="../assets/images/logo-dark-theme.svg"
      alt="Logo Dark"
    />

    <button
      @click="toggleTheme"
      class="p-2.5 bg-gray-100 dark:bg-gray-700 rounded-sm cursor-pointer"
    >
      <img v-if="!isDark" src="../assets/images/icon-moon.svg" alt="Moon" />
      <img v-if="isDark" src="../assets/images/icon-sun.svg" alt="Sun" />
    </button>
  </header>
</template>
