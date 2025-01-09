<template>
  <header class="shadow-sm transition-colors duration-300 bg-white dark:bg-gray-900">
    <div class="container mx-auto px-4 py-4 flex justify-between items-center">
      <h1 class="text-xl font-bold transition-colors duration-300 text-gray-800 dark:text-white">
        {{ language === 'pt' ? 'Meu Currículo' : 'My Curriculum' }}
      </h1>
      <div class="flex items-center space-x-4">
        <button
          @click="$emit('toggle-language')"
          class="font-bold py-2 px-4 rounded transition duration-300 bg-blue-500 hover:bg-blue-600 text-white dark:hover:bg-blue-700 dark:bg-green-600"
        >
          {{ language === 'pt' ? 'Translate to English' : 'Traduzir para Português' }}
        </button>
        <button
          @click="$emit('toggle-dark-mode')"
          class="p-2 rounded-full transition-colors duration-300 bg-gray-200 hover:bg-gray-300 dark:bg-gray-700 dark:hover:bg-gray-600"
          aria-label="Toggle dark mode"
        >
          <SunIcon v-if="isDark" class="w-6 h-6 text-yellow-400" />
          <MoonIcon v-else class="w-6 h-6 text-gray-600" />
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { computed } from 'vue';
import { SunIcon, MoonIcon } from 'lucide-vue-next';

const props = defineProps({
  language: {
    type: String,
    required: true
  },
  isDark: {
    type: Boolean,
    required: true
  }
});

const language = computed(() => props.language);
const isDark = computed(() => props.isDark);
</script>

