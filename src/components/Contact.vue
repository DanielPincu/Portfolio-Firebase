<template>
	<div class="flex justify-center items-center bg-blue-200 dark:bg-red-200 rounded-3xl shadow-xl mt-20 border-2 border-blue-300 dark:border-red-300" id="contact"
	data-aos="flip-right"
     data-aos-offset="1000"
     data-aos-duration="1000"
	>
	  <div class="container mx-auto">
		<div class="w-full p-8 my-4 md:px-12">
		  <div class="flex">
			<h1 class="justify-center text-3xl mx-auto py-10">Leave me a message<span class="animate-pulse">|</span></h1>
		  </div>
		  <div class="grid grid-cols-1 gap-5 md:grid-cols-2 my-5">
			<input v-model="formData.firstName" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" type="text" placeholder="First Name*" />
			<input v-model="formData.lastName" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" type="text" placeholder="Last Name*" />
			<input v-model="formData.email" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" type="email" placeholder="Email*" />
			<input v-model="formData.phone" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" type="tel" placeholder="Phone*" />
		  </div>
		  <div class="mb-5">
			<textarea v-model="formData.message" placeholder="The choice has always been yours..." class="w-full h-32 bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg focus:shadow-outline"></textarea>
		  </div>
		  <div class="my-2 w-1/2 lg:w-1/4">
			<button @click="handleSubmit" class="uppercase  text-sm font-bold tracking-wide p-3 text-white rounded-full w-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-600 shadow-lg border-b-2 border-slate-50">Leave Message</button>
		  </div>
		</div>
	  </div>
	</div>
	<!-- Modal -->
	<div :class="{ 'hidden': !showModal }" class="fixed z-10 inset-0 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
	  <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
		<div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>
		<span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
		<!-- Modal Content -->
		<div class="inline-block align-bottom bg-blue-300 dark:bg-gray-800 rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" role="dialog" aria-modal="true" aria-labelledby="modal-headline">
		  <div class="bg-blue-300 dark:bg-red-300 dark:text-black px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
			<div class="sm:flex sm:items-start">
			  <div class="mx-auto flex-shrink-0 flex items-center justify-center h-12 w-12 rounded-full bg-green-100 sm:mx-0 sm:h-10 sm:w-10">
				<!-- Heroicon name: check -->
				<svg class="h-6 w-6 text-green-600" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
				  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
				</svg>
			  </div>
			  <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
				<h3 class="text-lg leading-6 font-medium dark:text-black" id="modal-headline">
				  You made the right choice!
				</h3>
				<div class="mt-2">
				  <p class="text-sm  ">
					You are now down the rabbit hole. I will get back to you soon.
				  </p>
				</div>
			  </div>
			</div>
		  </div>
		  <div class="bg-blue-500 dark:bg-red-500 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
			<button @click="closeModal" type="button" class="w-full inline-flex justify-center rounded-full border border-transparent shadow-sm px-4 py-2 bg-blue-600 text-base font-medium text-white hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 sm:ml-3 sm:w-auto sm:text-sm">
			  Close
			</button>
		  </div>
		</div>
	  </div>
	</div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const formData = ref({
	firstName: '',
	lastName: '',
	email: '',
	phone: '',
	message: ''
  });
  
  const showModal = ref(false);
  
  const handleSubmit = () => {
	const { firstName, lastName, email, phone, message } = formData.value;
  
	if (!firstName || !lastName || !email || !phone || !message) {
	  alert('Please fill in all fields');
	  return;
	}
  
	console.log({
	  firstName,
	  lastName,
	  email,
	  phone,
	  message
	});
  
	showModal.value = true;
	clearForm();
  };
  
  const clearForm = () => {
	formData.value.firstName = '';
	formData.value.lastName = '';
	formData.value.email = '';
	formData.value.phone = '';
	formData.value.message = '';
  };
  
  const closeModal = () => {
	showModal.value = false;
  };
  </script>
  
  
  