<template>
    <div class="home-portfolio">
        <Navbar />

        <HeroSection />

        <SkillsSection />
        <EducationSection />
        <ProjectsSection />

        <Footer />
    </div>
</template>

<script setup>
import Navbar from '@/components/partials/Navbar.vue'
import HeroSection from '@/components/sections/Hero.vue'
import SkillsSection from '@/components/sections/Skills.vue'
import EducationSection from '@/components/sections/Education.vue'
import ProjectsSection from '@/components/sections/Projects.vue'
import Footer from '@/components/partials/Footer.vue'
</script>

<style scoped>
.home-portfolio {
    min-height: 100vh;
}
</style>
