<template>
    <section class="skills-section">
        <div class="container">
            <h2>Skills</h2>
            <div class="skills-grid">
                <div v-for="skill in skills" :key="skill.name" class="skill-card">
                    <h3>{{ skill.name }}</h3>
                    <p>{{ skill.level }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'

const skills = ref([
    { name: 'Laravel', level: 'Advanced' },
    { name: 'Vue.js', level: 'Intermediate' },
    { name: 'PHP', level: 'Advanced' },
    { name: 'MySQL', level: 'Intermediate' },
    { name: 'JavaScript', level: 'Intermediate' },
    { name: 'Git', level: 'Intermediate' }
])
</script>

<style scoped>
.skills-section {
    padding: 4rem 0;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
}

h2 {
    font-size: 2rem;
    margin-bottom: 2rem;
    text-align: center;
    color: white;
}

.skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
}

.skill-card {
    background: rgba(255, 255, 255, 0.9);
    border: 1px solid rgba(255, 255, 255, 0.2);
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
    backdrop-filter: blur(10px);
}

.skill-card h3 {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
}

.skill-card p {
    color: #666;
}
</style>
