<template>
  <div>
    <h1 class="font-bold text-2xl text-center pt-5">Info</h1>
    <div v-for="item in my_info" class="font-bold shadow-xl text-xl border-2 border-blue-300 dark:border-red-300 mx-5 mt-5 flex flex-col bg-blue-200 dark:bg-red-200 rounded-full items-center justify-end h-16">
      <p>{{ item.line1 }}</p>
      <p>{{ item.line2 }}</p>
    </div>
 
  </div>



  <div class="pt-10">
      <h1 class="font-bold text-2xl text-center pt-5">Languages</h1>
      <div v-for="item in languages" class="shadow-xl border-2 border-blue-300 dark:border-red-300 mx-5 my-5 flex flex-col bg-blue-200 dark:bg-red-200 rounded-full items-center h-16 justify-center">
        <h1 class="text-xl font-bold px-4">{{ item.line1 }}</h1>
        <div class="w-36 xl:w-56 2xl:w-64 bg-blue-300 dark:bg-red-300 rounded-full">
          <div class="bg-blue-500 dark:bg-red-500 text-xs font-bold text-center text-white p-1 leading-none rounded-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-600 shadow-lg border-b-2 border-slate-50" :style="{ width: item.line2 + '%' }">{{ item.line2 }}%</div>
        </div>
      </div>
    </div>
  

</template>

<script setup>
import { ref } from 'vue';
import { initializeApp } from "firebase/app";
import { firebaseConfig } from "/firebase"; 
import { getFirestore, collection, getDocs } from "firebase/firestore";

initializeApp(firebaseConfig);

const my_info = ref([]);
const languages = ref([]);

const db = getFirestore();


getDocs(collection(db, "my_info")).then((snapshot) => {   
    snapshot.forEach((doc) => {
        my_info.value.push(doc.data());
    });
});

getDocs(collection(db, "languages")).then((snapshot) => {   
    snapshot.forEach((doc) => {
        languages.value.push(doc.data());
    });
});

</script>
