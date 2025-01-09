<template>
  <div :class="{ 'dark': isDark }">
    <div class="min-h-screen bg-white dark:bg-gray-900 transition-colors duration-300">
      <Header 
        @toggle-language="toggleLanguage" 
        @toggle-dark-mode="toggleDarkMode"
        :language="currentLanguage"
        :isDark="isDark"
      />
      <main>
        <Introduction :language="currentLanguage" />
        <Skills :language="currentLanguage" />
      </main>
      <Footer/>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Header from './pages/Header.vue';
import Introduction from './pages/Introduction.vue';
import Skills from './pages/Skills.vue';
import Footer from './pages/Footer.vue';

const currentLanguage = ref('pt');
const isDark = ref(false);

const toggleLanguage = () => {
  currentLanguage.value = currentLanguage.value === 'pt' ? 'en' : 'pt';
};

const toggleDarkMode = () => {
  isDark.value = !isDark.value;
  localStorage.setItem('darkMode', isDark.value ? 'enabled' : 'disabled');
};

onMounted(() => {
  const darkModePreference = localStorage.getItem('darkMode');
  if (darkModePreference === 'enabled' || (!darkModePreference && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDark.value = true;
  }
});
</script>






