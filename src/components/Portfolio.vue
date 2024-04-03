<template>
  <div class="border-t-2 border-b-2 pb-20 border-zinc-200 pt-20" id="portfolio">
    <div>
      <h1 class="text-center text-4xl pb-10">Showcase</h1>
    </div>

    <!-- Dropdown menu for filtering -->
    <div class="text-center mb-6">
      <label for="category" class="block text-lg font-medium text-gray-700">Select a category:</label>
      <select v-model="selectedCategory" id="category" name="category" class="bg-blue-100 dark:bg-red-100 mt-1 block w-full py-2 px-3 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
        <option value="">All Categories</option>
        <option v-for="category in categories" :value="category">{{ category }}</option>
      </select>
    </div>

    <!-- Portfolio cards -->
    <div class="grid md:grid-cols-2 gap-10 mt-16">
      <div v-for="(item, index) in filteredCards" :key="index" class="suitcase-card cursor-pointer">
        <div class="suitcase-wrapper">
          <div class="suitcase bg-blue-200 dark:bg-red-200 rounded-3xl overflow-hidden border-2 border-blue-300 dark:border-red-300 shadow-xl">
            <div class="suitcase-top bg-blue-400 dark:bg-red-400 p-4 relative">
              <div class="handle bg-blue-600 dark:bg-red-700 w-6 h-2 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"></div>
            </div>
            <div class="suitcase-body hover:bg-blue-300 dark:hover:bg-red-300 ease-out duration-500 bg-blue-200 h-60 dark:bg-red-200 p-4" @click="toggleVisibility(index)">
              <h1 class="text-4xl text-gray-800 font-bold cursor-pointer mb-5 2xl:pl-5">{{ item.title }}</h1>
              <p class=" mb-5 2xl:px-5">{{ item.info }}</p>
            </div>
            <div v-show="visibleDiv[index]">
              <!-- Content to display when the card is expanded -->
              <a @click="openModal(item.remote_link, index)">
                <img :src="item.image_link" class="bg-blue-200 border-t-2 border-b-2 border-transparent hover:border-blue-500 hover:dark:border-red-500 dark:bg-red-200 ease-in-out duration-100">
              </a>
              <p class="bg-blue-200 dark:bg-red-200 p-10">{{ item.extra_info }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal component -->
    <div class="fixed inset-0 overflow-y-auto z-10" v-if="showModal">
      <div class="flex items-center justify-center min-h-screen pt-4 px-4 pb-20 text-center">
        <div class="fixed inset-0 transition-opacity" aria-hidden="true">
          <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
        </div>
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
        <div class="inline-block bg-white rounded-3xl text-left overflow-hidden shadow-xl transform transition-all my-8 align-middle w-[1200px]">
          <!-- Modal content -->
          <div class="bg-white px-4 pt-5 pb-4">
            <!-- Adjust your modal content here -->
            <iframe :src="modalContent" frameborder="0" allow="autoplay" allowfullscreen class="w-full h-[70vh]"></iframe>
          </div>
          <div class="bg-gray-50 px-4 py-3 flex flex-row-reverse">
            <button @click="showModal = false" type="button" class="my-5 inline-flex justify-center w-full rounded-full px-4 py-2 bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-600 font-medium text-white shadow-sm hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500 ml-3 text-sm">
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { initializeApp } from "firebase/app"; 
import { firebaseConfig } from "/firebase";
import { getFirestore, collection, getDocs } from "firebase/firestore";
import { getStorage, ref as storageRef, getDownloadURL } from 'firebase/storage';

const firebaseApp = initializeApp(firebaseConfig);
const db = getFirestore(firebaseApp);
const storage = getStorage(firebaseApp);

const selectedCategory = ref('');
const visibleDiv = ref([]);
const cards = ref([]);

const getDownloadUrl = async (imagePath) => {
  try {
    const imageRef = storageRef(storage, imagePath);
    return await getDownloadURL(imageRef);
  } catch (error) {
    console.error('Error retrieving image URL:', error);
    return null;
  }
};

getDocs(collection(db, "cards")).then(async (snapshot) => {
  snapshot.forEach(async (doc) => {
    const cardData = doc.data();
    const imageUrl = await getDownloadUrl(cardData.image_link);
    cards.value.push({ ...cardData, image_link: imageUrl });
  });

  visibleDiv.value = Array(cards.value.length).fill(false);
});

const categories = computed(() => {
  const uniqueCategories = new Set();
  cards.value.forEach(card => {
    uniqueCategories.add(card.category);
  });
  return Array.from(uniqueCategories);
});

const filteredCards = computed(() => {
  if (!selectedCategory.value) {
    return cards.value;
  } else {
    return cards.value.filter(card => card.category === selectedCategory.value);
  }
});

const toggleVisibility = (index) => {
  visibleDiv.value.forEach((value, i) => {
    if (i !== index) {
      visibleDiv.value[i] = false;
    }
  });
  visibleDiv.value[index] = !visibleDiv.value[index];
};

const showModal = ref(false);
const modalContent = ref('');

const openModal = async (content, index) => {
  toggleVisibility(index);
  if (content.startsWith('http://') || content.startsWith('https://')) {
    modalContent.value = content;
  } else if (content.startsWith('gs://')) {
    try {
      const downloadUrl = await getDownloadUrl(content);
      if (downloadUrl) {
        modalContent.value = downloadUrl;
      } else {
        console.error('Error converting GS link to download URL.');
      }
    } catch (error) {
      console.error('Error converting GS link to download URL:', error);
    }
  } else {
    console.error('Invalid content format. Expected a URL or GS link.');
  }
  showModal.value = true;
};
</script>
