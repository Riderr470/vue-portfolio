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
        institution: 'American International University Bangladesh',
        year: '2019 - 2024',
        description: 'Focused on web development and software engineering'
    },
    {
        id: 2,
        degree: 'Higher Secondary Certificate',
        institution: 'Uttara Eminence College',
        year: '2017 - 2018',
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
}

.education-list {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.education-item {
    background: var(--secondary);
    padding: 2rem;
    border-radius: 8px;
    border-left: 4px solid var(--tertiary);
    backdrop-filter: blur(10px);
}

.education-item h3 {
    font-size: 1.3rem;
    margin-bottom: 0.5rem;
}

.education-item h4 {
    font-size: 1.1rem;
    margin-bottom: 0.5rem;
}

.year {
    color: var(--text-base);
    font-size: 0.9rem;
    margin-bottom: 1rem;
}
</style>
