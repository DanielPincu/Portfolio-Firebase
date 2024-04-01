<template>
  <div class="border-b-2 border-zinc-200 pb-20" id="about">
    <div class="shadow-xl rounded-3xl mt-20 px-5 2xl:px-14 pb-20 bg-blue-200 dark:bg-red-200 border-2 border-blue-300 dark:border-red-300" 
    
     data-aos="flip-right"
     data-aos-offset="700"
     data-aos-duration="1100"
     >
      <div>
        <div class="flex justify-center">
          <h1 class="text-4xl py-10">About Me</h1>
        </div>
        <div class="grid xl:grid-cols-2 gap-10 grid-cols-1">
          <div>
            <p v-for="(paragraph, index) in paragraphs" :key="index" class="mb-5 max-2xl:pl-5">{{ paragraph }}</p>
          </div>
          <div class="hidden lg:block">
            <img class="rounded-3xl" :src="imageSrc" alt="">
          </div>
        </div>

        <button v-if="!isReadMore" class="py-5 px-5" @click="toggleReadMore">{{ buttonText }}</button>

        <div v-show="isReadMore">
          <p class="py-10 pl-5 italic md:mx-20" v-for="(paragraph, index) in extraParagraphs" :key="index">{{ paragraph }}</p>
          <button class="px-5" @click="toggleReadMore">{{ buttonText }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { paragraphs, extraParagraphs, imageSrc } from '../modules/about.js';

const isReadMore = ref(false);

const toggleReadMore = () => {
  isReadMore.value = !isReadMore.value;
};

const buttonText = computed(() => {
  return isReadMore.value ? '' : 'VUE more...';
});
</script>

<style>
/* Your component styles here */
</style>
