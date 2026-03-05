<template>
    <section class="education-section">
        <div class="container">
            <h2>Education</h2>
            <div class="education-list">
                <div v-for="edu in education" :key="edu.id" class="education-item">
                    <h3>{{ edu.degree }}</h3>
                    <h4>{{ edu.institution }}</h4>
                    <p class="year">{{ edu.year }}</p>
                    <p>{{ edu.description }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'

const education = ref([
    {
        id: 1,
        degree: 'Bachelor of Science in Computer Science',
        institution: 'Your University Name',
        year: '2018 - 2022',
        description: 'Focused on web development and software engineering'
    },
    {
        id: 2,
        degree: 'Higher Secondary Certificate',
        institution: 'Your College Name',
        year: '2016 - 2018',
        description: 'Science background with focus on mathematics and computer science'
    }
])
</script>

<style scoped>
.education-section {
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

.education-list {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.education-item {
    background: rgba(255, 255, 255, 0.9);
    padding: 2rem;
    border-radius: 8px;
    border-left: 4px solid rgba(255, 255, 255, 0.5);
    backdrop-filter: blur(10px);
}

.education-item h3 {
    font-size: 1.3rem;
    margin-bottom: 0.5rem;
}

.education-item h4 {
    font-size: 1.1rem;
    color: #667eea;
    margin-bottom: 0.5rem;
}

.year {
    color: #666;
    font-size: 0.9rem;
    margin-bottom: 1rem;
}
</style>
