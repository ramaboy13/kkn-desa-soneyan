<script setup>
import FaqSection from './components/FaqSection.vue'
import FoodSection from './components/FoodSection.vue'
import FooterApp from './components/FooterApp.vue'
import HeroSection from './components/HeroSection.vue'
import KontakSection from './components/KontakSection.vue'
import NavBar from './components/NavBar.vue'
import TentangSection from './components/TentangSection.vue'
</script>

<template>
  <main>
    <!-- NavBar -->
    <NavBar></NavBar>

    <!--Home Section-->
    <HeroSection></HeroSection>

    <!--Section Tentang Kami-->
    <TentangSection></TentangSection>

    <!--Section Menu Makanan-->
    <FoodSection></FoodSection>

    <!--Section FAQ-->
    <FaqSection></FaqSection>

    <!--Section Team-->
    <KontakSection></KontakSection>

    <!-- Footer -->
    <FooterApp></FooterApp>
  </main>
</template>
