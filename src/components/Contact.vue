<template>
	<div class="flex justify-center items-center bg-blue-200 dark:bg-red-200 rounded-3xl shadow-xl mt-20 mb-5 border-2 border-blue-300 dark:border-red-300 crd-blue crd-red" id="contact" data-aos="flip-right" data-aos-duration="1000">
	  <div class="container mx-auto">
		<h1 class="flex justify-center text-3xl mx-auto py-10">Drop me a message<span class="animate-pulse">|</span></h1>
		<form target="_blank" action="https://formspree.io/f/mgegplkr" method="POST" class="w-full p-8 my-4 md:px-12">
		  <div class="grid grid-cols-1 gap-5 md:grid-cols-2 my-5">
			<input type="text" name="name" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" placeholder="Full Name" required>
			<input type="email" name="email" class="w-full bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg" placeholder="Email Address" required>
		  </div>
		  <div class="mb-5">
			<textarea placeholder="Your Message" class="w-full h-32 bg-gray-200 text-gray-900 mt-2 p-3 rounded-lg focus:shadow-outline" name="message" rows="10" required></textarea>
		  </div>
		  <button type="submit" class="uppercase text-sm font-bold tracking-wide p-3 text-white rounded-full w-full bg-gradient-to-r from-blue-400 to-blue-600 dark:from-red-400 dark:to-red-600 shadow-lg border-b-2 border-slate-50">Submit Form</button>
		</form>
	  </div>
	</div>
  </template>
