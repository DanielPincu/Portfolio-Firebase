<template>  
  <div class="pt-10 border-zinc-200 xl:flex justify-center hidden">
    <h1 class="text-4xl pt-5 pb-16" 
     data-aos="flip-right"
     data-aos-easing="ease-in-back"
     data-aos-duration="500"
     data-aos-offset="700"
     >{{ pageTitle.title }}</h1>
  </div>

  <div class="xl:grid md:grid-cols-4 grid-cols-2 items-center gap-5 md:pb-10 mb-16 hidden" 

     data-aos="flip-right"
     data-aos-duration="1000"
     data-aos-easing="ease-in-back"
     data-aos-offset="700">

    <div v-for="(service, index) in services" :key="index" @click="toggleVisibility(index)" class=" cursor-pointer border-2 border-blue-300 dark:border-red-300 bg-blue-200 dark:bg-red-200 rounded-3xl drop-shadow-xl h-60 flex flex-col items-center mb-10 hover:scale-[103%] duration-500">
      <h1 class="text-2xl text-blue-500 dark:text-red-500 text-center pt-10">{{ service.title }}</h1>
      <svg class="text-blue-500 dark:text-red-500 w-32 md:w-64 justify-center" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" :d="service.svgPath" />
      </svg>
      <div v-show="visibleDiv === index" class="animate-bounce bg-blue-300 dark:bg-red-300 rounded-3xl drop-shadow-xl h-60 flex flex-col items-center mb-2 w-full">
        <h1 class="text-xl p-5">{{ service.description }}</h1>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { services } from '../modules/services';
import { pageTitle } from '../modules/services';


const visibleDiv = ref(null);
const toggleVisibility = (index) => {
  visibleDiv.value = visibleDiv.value === index ? null : index;
};
</script>
