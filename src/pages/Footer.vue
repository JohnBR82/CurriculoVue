<template>
  <footer class="bg-gray-800 text-white py-8">
    <div class="container mx-auto px-4 flex flex-col md:flex-row justify-between items-center">
      <div class="mb-4 md:mb-0">
        <a href="https://github.com/JohnBR82" target="_blank" rel="noopener noreferrer" class="hover:text-gray-300 transition duration-300">
          <GithubIcon class="inline-block mr-2" />
          GitHub
        </a>
      </div>
      <div class="text-sm">
        &copy; {{ new Date().getFullYear() }} Gabriel. Todos os direitos reservados.
      </div>
    </div>
  </footer>
</template>

<script setup>
import { GithubIcon } from 'lucide-vue-next';
</script>