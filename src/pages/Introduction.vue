<template>
  <section class="container mx-auto px-4 py-12 flex flex-col md:flex-row items-center">
    <div class="md:w-1/2 mb-8 md:mb-0">
      <h2 class="text-3xl font-bold text-gray-800 dark:text-white mb-4">
        {{ language === 'pt' ? 'Olá, eu sou Gabriel Silva' : 'Hello, I am Gabriel Silva' }}
      </h2>
      <p class="text-gray-800 dark:text-white leading-relaxed">
        {{ 
          language === 'pt' 
            ? 'Desenvolvedor web apaixonado por criar soluções inovadoras e eficientes. Com experiência em Vue.js, React e Node.js, estou sempre em busca de novos desafios e oportunidades de aprendizado.' 
            : 'Web developer passionate about creating innovative and efficient solutions. With experience in Vue.js, React.js, and Node.js, I am always looking for new challenges and learning opportunities.'
        }}
      </p>
    </div>
    <div class="md:w-1/2">
      <img src="../assets/image2.png" alt="Profile" class="rounded-full mx-auto" oncontextmenu="return false;" />
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps(['language']);
const language = computed(() => props.language);


</script>