<template>
  <section class="container mx-auto px-4 py-12">
    <div class="flex flex-wrap justify-center space-x-4 mb-8">
      <button
        v-for="(skill, index) in skills"
        :key="index"
        @click="currentSkill = index"
        class=" bg-[#1e90ff] dark:bg-[#32cd32] dark:text-white font-bold py-2 px-4 rounded transition duration-300 mb-2"
        :class="{ 'text-white dark:text-[#111111]': currentSkill === index }"
      >
        {{ skill.name[language] }}
      </button>
    </div>
    <div class="text-center">
      <h3 class="text-2xl font-bold dark:text-white text-gray-800 mb-4">{{ skills[currentSkill].name[language] }}</h3>
      <div class="text-gray-600 mb-4 dark:text-white font-serif" v-html="formatDescription(skills[currentSkill].description[language])"></div>
      
      <div v-if="currentSkill === 0" class="mb-72">
        <h4 class="text-xl font-semibold text-gray-700 mb-4 dark:text-white font-mono">{{ language === 'pt' ? 'Minhas habilidades em Programação' : 'My Programming Skills' }}</h4>
        <div class="w-full max-w-md mx-auto h-64">
          <Pie v-if="loaded" :data="chartData" :options="chartOptions" />
          <Pie class="mt-8" v-if="loaded" :data="chartData2" :options="chartOptions" />
        </div>
      </div>
      
      <a
        :href="skills[currentSkill].link"
        target="_blank"
        rel="noopener noreferrer"
        class="text-blue-500 hover:text-blue-600 transition duration-300"
      >
        {{ language === 'pt' ? 'Saiba mais' : 'Learn more' }}
      </a>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js';
import { Pie } from 'vue-chartjs';

ChartJS.register(ArcElement, Tooltip, Legend);

const props = defineProps(['language']);
const language = computed(() => props.language);

const currentSkill = ref(0);
const loaded = ref(false);

const skills = [
  {
    name: { pt: 'Habilidades', en: 'Skills' },
    description: {
      pt: 'Habilidades adquiridas ao longo de 4 anos de programação.<br>Experiência em desenvolvimento web e mobile.',
      en: 'Skills acquired over 4 years of programming.<br>Experience in web and mobile development.'
    },
    link: 'https://github.com/JohnBR82'
  },
  {
    name: { pt: 'Experiencia', en: 'Experience' },
    description: {
      pt: 'Supermercado Atacadao - CLT<br> 3 meses <br> Trabalhando 8h por dia na frente de caixa, oferecendo apoio a outros setores, carregando carrinhos. <br><br> KODA X - Freelance <br> 5 meses <br> Trabalhando como Desenvolvedor Frontend freelancer<br> Ofereço telas com responsividade e inovadoras para os clientes da empresa, estando num contrato informal <br><br> Freelancer Informal <br> 2 anos <br> Como freelancer informal, ofereci meus serviços a mais de 20 clientes, entregando inovação e responsividade',
      en: 'Atacadao Supermarket - CLT<br> 3 months <br> Working 8 hours a day at the cash register, providing support to other departments, and loading carts. <br><br> KODA X - Freelance <br> 5 months <br> Working as a Freelance Frontend Developer. I provide responsive and innovative designs for the company clients, under an informal contract. <br><br> Informal Freelancer <br> 2 years <br> As an informal freelancer, I offered my services to over 20 clients, delivering innovation and responsiveness.'
    },
    link: 'https://github.com/JohnBR82'
  },
  {
    name: { pt: 'Projetos', en: 'Projects' },
    description: {
      pt: 'Techsolucoes - HTML + TailwindCSS <br> Inicialmente desenvolvido por mim como um site de um trabalho freelancer para uma pequena farmaceutica, mas refeito por motivo da lei LGPD <br> melhorado no processo tendo sistema de tradução e login bem consistente e api do google maps para localização, contendo 9 paginas <br><br> TradeConnect - React<br> Tradeconnect é uma landing page demonstrativa, para demonstrar habilidades para cliente, site usa flat design para atrair olhares de empresa <br><br> Reprodutor De Musica - Vue + TailwindCSS <br> é um reprodutor de musica brasileira simples e com intuitiva para parecer com Spotify para fins de aprendizado e demonstração <br> ',
      en: 'Techsolucoes - HTML + Tailwind css <br> Initially developed by me as a freelance project for a small pharmaceutical company, but redesigned due to CCPA or GDPR law <br> Improved in the process with a consistent translation and login system, and Google Maps API for location, containing 9 pages <br><br> TradeConnect - React <br> Tradeconnect is a demonstrative landing page, showcasing skills for clients, using a flat design to attract company attention <br><br> Music Player - Vue <br> A simple and intuitive Brazilian music player resembling Spotify for learning and demonstration purposes <br> '
    },
    image: '/placeholder.svg?height=100&width=100',
    link: 'https://github.com/yourusername',
    projectLinks: {
      pt: [
        { name: 'Techsolucoes', url: 'https://techsolutions-website.vercel.app/' },
        { name: 'TradeConnect', url: 'https://tradeconnect.vercel.app/' },
        { name: 'Reprodutor De Musica', url: 'https://reprodutordemusicavue.vercel.app/' }
      ],
      en: [
        { name: 'Techsolucoes', url: 'https://techsolutions-website.vercel.app/' },
        { name: 'TradeConnect', url: 'https://tradeconnect.vercel.app/' },
        { name: 'Music Player', url: 'https://reprodutordemusicavue.vercel.app/' }
      ]
    }
  },
  {
    name: { pt: 'Outros Projetos/Serviços', en: 'Other Projects/Services' },
    description: {
      pt: 'Estive fazendo pequenas ferramentas para cmd que está disponivel no meu github, como renomear pastas automaticamente e outros programas simples <br> Tenho feito freelancer de criação de arte e ensinar pessoas a utilizar stable diffusion ferramenta de arte por IA <br> Criei modificações para jogos de pc, afim de estudos de desenvolvimento de jogos <br> Desenvolvi designs de website para vender e outros serviços',
      en: 'I have been creating small command-line tools available on my GitHub, such as automatically renaming folders and other simple programs <br> I have been freelancing in creating art and teaching people how to use Stable Diffusion, an AI art tool <br> I have created modifications for PC games as part of my game development studies <br> I have developed website designs for sale and other services'
    },
    link: 'https://github.com/JohnBR82'
  }
];

const chartData = {
  labels: ['Javascript', 'Python', 'Java', 'C#','PHP'],
  datasets: [
    {
      backgroundColor: ['#F0DB4F', '#306998', '#f89820', '#9179E4', '#6c78af'],
      data: [30, 30, 15, 10, 15]
    }
  ]
};

const chartData2 = {
  labels: ['Vue.js', 'React', 'Angular', 'Django', 'Laravel', 'Node.js'],
  datasets: [
    {
      backgroundColor: ['#41b883', '#61dbfb', '#b52e31', '#092e20', '#f05340', '#3c873a'],
      data: [25, 25, 5, 5, 10, 30]
    }
  ]
};

const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  animation: {
    animateRotate: true,
    animateScale: true
  },
  plugins: {
    legend: {
      position: 'bottom'
    },
    tooltip: {
      callbacks: {
        label: (context) => {
          const label = context.label || '';
          const value = context.parsed || 0;
          return `${label}: ${value}%`;
        }
      }
    }
  }
};

const formatDescription = (description) => {
  if (currentSkill.value === 2) { // For the 'Projects' skill
    const links = skills[2].projectLinks[language.value];
    links.forEach(link => {
      const regex = new RegExp(link.name, 'g');
      description = description.replace(regex, `<a href="${link.url}" target="_blank" rel="noopener noreferrer" class="text-blue-500 hover:text-blue-600 transition duration-300">${link.name}</a>`);
    });
  }
  return description;
};

onMounted(() => {
  loaded.value = true;
});
</script>
