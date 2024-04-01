<template>
  <div class="flex justify-center sticky top-[100px]">
   <label class="inline-flex items-center cursor-pointer pt-20">
     <input type="checkbox" value="" class="sr-only peer">
     <div @click="toggleDark()" class="relative w-11 h-6 bg-red-700  rounded-full peer dark:bg-red-600 peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-blue-600"></div>
   </label>
  </div>
  
 
   <div class="mt-10 sticky top-[300px] mb-5">
     <div v-for="(navItem, index) in navItems" :key="index" class="flex justify-evenly items-center my-5">
       <a @click="scrollTo(navItem.href, $event)" class="text-xl font-bold text-blue-900 cursor-pointer hover:scale-110 hover:transition ease-in-out duration-700">{{ navItem.label }}</a>
     </div>
   </div>
 </template>
 
 <script setup>
 import { useDark, useToggle } from "@vueuse/core"
 import { navItems } from "../modules/nav.js";
 
 const isDark = useDark()  
 const toggleDark = useToggle(isDark)
 
 const scrollTo = (target, event) => {
   event.preventDefault();
   const element = document.querySelector(target);
   if (element) {
     const offsetTop = element.offsetTop;
     window.scrollTo({
       top: offsetTop,
       behavior: "smooth"
     });
   }
 };
 </script>
 