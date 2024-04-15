<template>
  
  <div class="lg:hidden sticky top-0 z-10 bg-blue-100 dark:bg-red-700 -mx-5">
      <div class="flex justify-center items-center mt-10">
        <div class="flex my-5">
          <div v-for="(navItem, index) in navItems" :key="index" class="mx-3">
            <a @click="scrollTo(navItem.href, $event)" class="text-lg dark:text-slate-200 font-bold cursor-pointer hover:scale-110 hover:transition ease-in-out duration-700">{{ navItem.label }}</a>
          </div>
        </div>
      </div>
    </div>

  <div class="relative tt" data-aos="flip-right" data-aos-duration="1000">
    
    <img class="rounded-full blink border-blue-500 dark:border-red-500 mx-auto w-[90%] m-10 dark:scale-x-[-1]" src="/assets/img/matrix.jpeg" alt="">

   
    <div class="absolute inset-0 flex flex-col justify-center items-center text-center" id="home">
      <h1 class="text-sm md:text-xl pb-10 xl:text-3xl font-bold dark:text-slate-200 text-white">
        I’m Daniel Pincu <br>
        <span class="text-blue-500 dark:text-red-500">Front-end Developer</span>
      </h1>

     
      <label class="inline-flex items-center lg:hidden cursor-pointer">
        <input type="checkbox" value="" class="sr-only peer" v-model="isDark">
        <div class="relative w-11 h-6 bg-red-700 rounded-full peer dark:bg-red-600 peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-blue-600"></div>
      </label>

    
      <p class="text-xl md:text-3xl xl:text-5xl pl-3 mb-1 text-slate-200">Welcome to the Matrix<span class="animate-pulse">|</span></p>

      <div class="flex md:pt-5 2xl:pt-24">
  <button @click="openModal('Download')" class="blink-red hidden dark:block button bg-red-500  shadow-lg border-b-2 border-slate-50 text-white font-bold text-sm md:text-xl px-5 md:py-6 2xl:px-0 rounded-full w-38 md:w-44 mr-2 md:mr-44 2xl:mr-64">
    <span>Fetch CV</span>
    <div class="liquid"></div>
  </button>
  <button @click="openModal('Watch')" class="blink-blue block dark:hidden button bg-blue-500 shadow-lg border-b-2 border-slate-50 text-white font-bold text-sm md:text-xl px-5 md:py-6 2xl:px-0 rounded-full w-38 md:w-44 mr-2 md:mr-44 2xl:mr-64">
    <span>Watch CV</span>
    <div class="liquid2"></div>
  </button>
  <button @click="openModal('Watch')" class="blink-blue hidden dark:block button bg-blue-500 shadow-lg border-b-2 border-slate-50 text-white font-bold text-sm md:text-xl px-5 md:py-6 2xl:px-0 rounded-full w-38 md:w-44">
    <span>Watch CV</span>
    <div class="liquid2"></div>
  </button>
  <button @click="openModal('Download')" class="blink-red block dark:hidden button bg-red-500 shadow-lg border-b-2 border-slate-50 text-white font-bold text-sm md:text-xl px-5 md:py-6 2xl:px-0 rounded-full w-38 md:w-44">
    <span>Fetch CV</span>
    <div class="liquid"></div>
  </button>
</div>
    </div>
  </div>

  <!-- Modal -->
 
  <div v-if="showModal" class="fixed inset-0 z-50 overflow-auto bg-black bg-opacity-75 flex justify-center items-center">
    <div class="bg-white dark:bg-slate-600 rounded-lg p-8">
      
      <div v-if="isVideoCvVisible" class="mb-4">
        <h3 class="text-lg font-bold mb-2">Video CV</h3>
        <video controls autoplay class=" w-64 xl:w-[1000px] xl:h-[500px] " :src="modalUrl" alt="Video CV"></video>
      </div>
      
      
      <div v-if="isDownloadCvVisible">
        <iframe :src="modalUrl" class="w-64 h-32 xl:w-[1000px] xl:h-[500px]" frameborder="0"></iframe>
        <a :href="modalUrl" class="text-blue-500 dark:text-red-500">Fetch CV</a>
      </div>
      <button @click="closeModal" class="mt-4 px-4 py-2 text-sm w-full bg-blue-500 dark:bg-red-500 rounded-full text-white hover:bg-blue-600 hover:dark:bg-red-600 hover:scale-[101%] duration-300 border-b-2 border-slate-200">Close</button>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue';
import { navItems } from '../modules/nav';
import { useDark } from "@vueuse/core";
import { initializeApp } from "firebase/app";
import { firebaseConfig } from "/firebase"; 
import { getFirestore, collection, getDocs } from "firebase/firestore";
import { getStorage, ref as storageRef, getDownloadURL } from 'firebase/storage';

initializeApp(firebaseConfig);

const cv = ref([]);
const video = ref([]);
const loading = ref(true); 
const modalUrl = ref('');

const db = getFirestore();
const storage = getStorage();

getDocs(collection(db, "hero")).then((snapshot) => {   
    snapshot.forEach(async (doc) => {
        const data = doc.data();

        try {
            // Get the download URL for cv
            const cvUrl = await getDownloadURL(storageRef(storage, data.text_cv));
            const videoUrl = await getDownloadURL(storageRef(storage, data.video_cv));

            // Push the URL to the cv and video arrays
            cv.value.push({ url: cvUrl, name: "cv.pdf" });
            video.value.push({ url: videoUrl, name: "video.mp4" });

            loading.value = false; // Set loading state to false once data is fetched
        } catch (error) {
            console.error("Error fetching data:", error);
        }
    });    
});

const isDark = useDark();


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


const showModal = ref(false);
const isVideoCvVisible = ref(false);
const isDownloadCvVisible = ref(false);

const openModal = (action) => {
  showModal.value = true;
  if (action === 'Watch') {
    isVideoCvVisible.value = true;
    isDownloadCvVisible.value = false;
    modalUrl.value = video.value[0]?.url;
  } else {
    isVideoCvVisible.value = false;
    isDownloadCvVisible.value = true;
    modalUrl.value = cv.value[0]?.url;
  }
};

const closeModal = () => {
  showModal.value = false;
  isVideoCvVisible.value = false;
  isDownloadCvVisible.value = false;
};
</script>

<style>
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.1;
  }
}

.animate-pulse {
  animation: pulse 0.3s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>
