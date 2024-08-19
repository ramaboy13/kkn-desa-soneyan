<script setup>
import FoodSection from './components/FoodSection.vue'
import FooterApp from './components/FooterApp.vue'
import HeroSection from './components/HeroSection.vue'
import KontakSection from './components/KontakSection.vue'
import NavBar from './components/NavBar.vue'
import TeamSection from './components/TeamSection.vue'
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

    <!--Section Team-->
    <TeamSection></TeamSection>

    <!--Section Team-->
    <KontakSection></KontakSection>

    <!-- Footer -->
    <FooterApp></FooterApp>
  </main>
</template>
