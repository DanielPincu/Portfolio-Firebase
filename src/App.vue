<script setup>
import { onMounted } from 'vue';
import CV from './components/CV.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import Nav from './components/Nav.vue'
import Portfolio from './components/Portfolio.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import anime from 'animejs'

onMounted(() => {
  anime({
    targets: '.tt',
    opacity: [0, 1],
    translateY: [-900, 0],
    translateX: [0, 0], 
    easing: "linear",
    duration: 1000,
  });


});

import AOS from 'aos';
import 'aos/dist/aos.css'; // Import AOS CSS file
AOS.init({
    once: true,
});





</script>



<template>
   

<main class="lg:grid grid-cols-12">


<!-- Left Column -->
    <div class="col-span-3 hidden lg:block pb-5 border-r-2 border-zinc-200 dark:border-zinc-700">
        
        <CV />

    </div>


<!-- Center Column -->
    <div class="lg:col-span-8 col-span-12 mx-5">
        <Hero />
        <Services />
        <Portfolio />
        <About />
        <Contact />

    </div>
    

<!-- Right Column -->
    <div class="col-span-1 hidden lg:block rounded-full xl:bg-blue-200 dark:bg-red-500 border-2 border-blue-300 xl:dark:border-red-700 crd-red crd-blue" 
    
    data-aos="fade-left"
    data-aos-duration="2000"
    
    >

        <Nav />

    </div>



</main>
    
  
<Footer />


</template>

