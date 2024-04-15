
<!-- DO NOT DELETE, Case study :) -->
<!-- <script setup>
import { ref } from 'vue';
import { initializeApp } from "firebase/app";
import { firebaseConfig } from "/firebase"; 
import { getFirestore, collection, getDocs } from "firebase/firestore";

initializeApp(firebaseConfig);

const my_info = ref([]);
const languages = ref([]);
const skills = ref([]);
const tools = ref([]);
const hobbies = ref([]);

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

getDocs(collection(db, "skills")).then((snapshot) => {   
    snapshot.forEach((doc) => {
        skills.value.push(doc.data());
    });
});

getDocs(collection(db, "tools")).then((snapshot) => {   
    snapshot.forEach((doc) => {
        tools.value.push(doc.data());
    });
});

getDocs(collection(db, "hobbies")).then((snapshot) => {   
    snapshot.forEach((doc) => {
        hobbies.value.push(doc.data());
    });
});

</script> -->


<template>
  <div v-if="databaseLoaded">
    <div class="flex justify-center" data-aos="fade-right">
      <img class="w-48 mt-10" src="/public/assets/img/ddd.png">
    </div>
    <div class="border-b-2 border-zinc-200 dark:border-zinc-700 pb-5 mb-16" data-aos="fade-right" data-aos-duration="1000">
      <h1 v-if="databaseLoaded" class="text-2xl font-bold text-center dark:text-slate-200 mt-5" data-aos="fade-up">Daniel Pincu</h1>
      <p v-if="databaseLoaded" class="text-center text-gray-500 dark:text-slate-200" data-aos="fade-up">Front-end developer</p>
    </div>

    <div>
      <div v-for="item in my_info" class="crd-blue crd-red shadow-xl text-xl border-2 border-blue-300 dark:border-red-600 mx-5 mt-5 flex flex-col bg-blue-200 dark:bg-red-500 dark:text-slate-200 rounded-full items-center justify-end h-16" data-aos="fade-up" data-aos-duration="2000">
        <p class="font-bold">{{ item.line1 }}</p>
        <p>{{ item.line2 }}</p>
      </div>
    </div>

    <div class="pt-10">
      <h1 v-if="databaseLoaded" class="font-bold text-2xl text-center dark:text-slate-200 pt-5" data-aos="fade-up">Languages</h1>
      <div v-for="item in languages" class="crd-blue crd-red shadow-xl border-2 border-blue-300 dark:border-red-600 mx-5 my-5 flex flex-col bg-blue-200 dark:bg-red-500 rounded-full items-center h-16 justify-center" data-aos="fade-up" data-aos-duration="2000">
        <h1 class="text-xl font-bold dark:text-slate-200 px-4">{{ item.line1 }}</h1>
        <div class="w-36 xl:w-56 2xl:w-64 bg-blue-300 dark:bg-red-300 rounded-full">
          <div class="bg-blue-500 dark:bg-red-500 text-xs font-bold text-center text-slate-200 p-1 leading-none rounded-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-700 shadow-lg border-b-2 border-slate-50" :style="{ width: item.line2 + '%' }">{{ item.line2 }}%</div>
        </div>
      </div>
    </div>

    <div class="pt-10">
      <h1 v-if="databaseLoaded" class="font-bold text-2xl text-center dark:text-slate-200 pt-5" data-aos="fade-up">Skills</h1>
      <div v-for="item in skills" class="crd-blue crd-red shadow-xl border-2 border-blue-300 dark:border-red-600 mx-5 my-5 flex flex-col bg-blue-200 dark:bg-red-500 rounded-full items-center h-16 justify-center" data-aos="fade-up" data-aos-duration="2000">
        <h1 class="text-xl font-bold px-4 dark:text-slate-200">{{ item.line1 }}</h1>
        <div class="w-36 xl:w-56 2xl:w-64 bg-blue-300 dark:bg-red-300 rounded-full">
          <div class="bg-blue-500 dark:bg-red-500 text-xs font-bold text-center text-slate-200 p-1 leading-none rounded-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-700 shadow-lg border-b-2 border-slate-50" :style="{ width: item.line2 + '%' }">{{ item.line2 }}%</div>
        </div>
      </div>
    </div>

    <div class="pt-10">
      <h1 v-if="databaseLoaded" class="font-bold text-2xl text-center dark:text-slate-200 pt-5" data-aos="fade-up">Tools</h1>
      <div v-for="item in tools" class="crd-blue crd-red shadow-xl border-2 border-blue-300 dark:border-red-600 mx-5 my-5 flex flex-col bg-blue-200 dark:bg-red-500 rounded-full items-center h-16 justify-center" data-aos="fade-up" data-aos-duration="2000">
        <h1 class="text-xl font-bold px-4 dark:text-slate-200">{{ item.line1 }}</h1>
        <div class="w-36 xl:w-56 2xl:w-64 bg-blue-300 dark:bg-red-300 rounded-full">
          <div class="bg-blue-500 dark:bg-red-500 text-xs font-bold text-center text-slate-200 p-1 leading-none rounded-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-700 shadow-lg border-b-2 border-slate-50" :style="{ width: item.line2 + '%' }">{{ item.line2 }}%</div>
        </div>
      </div>
    </div>

   
  </div>

  <div class="pt-10 sticky top-0">
      <h1 v-if="databaseLoaded" class="font-bold text-2xl text-center dark:text-slate-200 pt-5" data-aos="fade-up">Hobbies</h1>
      <div v-for="item in hobbies" class="crd-blue crd-red shadow-xl border-2 border-blue-300 dark:border-red-600 mx-5 my-5 flex flex-col bg-blue-200 dark:bg-red-500 rounded-full items-center h-16 justify-center" data-aos="fade-up" data-aos-duration="2000">
        <h1 class="text-xl font-bold px-4 dark:text-slate-200">{{ item.line1 }}</h1>
        <div class="w-36 xl:w-56 2xl:w-64 bg-blue-300 dark:bg-red-300 rounded-full">
          <div class="bg-blue-500 dark:bg-red-500 text-xs font-bold text-center text-slate-200 p-1 leading-none rounded-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-700 shadow-lg border-b-2 border-slate-50" :style="{ width: item.line2 + '%' }">{{ item.line2 }}%</div>
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
const skills = ref([]);
const tools = ref([]);
const hobbies = ref([]);
const databaseLoaded = ref(false);

const db = getFirestore();

Promise.all([
  getDocs(collection(db, "my_info")),
  getDocs(collection(db, "languages")),
  getDocs(collection(db, "skills")),
  getDocs(collection(db, "tools")),
  getDocs(collection(db, "hobbies"))
])
.then(([myInfoSnapshot, languagesSnapshot, skillsSnapshot, toolsSnapshot, hobbiesSnapshot]) => {   
  myInfoSnapshot.forEach((doc) => {
    my_info.value.push(doc.data());
  });

  languagesSnapshot.forEach((doc) => {
    languages.value.push(doc.data());
  });

  skillsSnapshot.forEach((doc) => {
    skills.value.push(doc.data());
  });

  toolsSnapshot.forEach((doc) => {
    tools.value.push(doc.data());
  });

  hobbiesSnapshot.forEach((doc) => {
    hobbies.value.push(doc.data());
  });

  databaseLoaded.value = true;
});
</script>
