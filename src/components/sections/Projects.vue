<template>
    <section class="projects-section">
        <div class="container">
            <h2>Projects</h2>
            <div class="projects-grid">
                <div v-for="project in projects" :key="project.id" class="project-card">
                    <h3>{{ project.title }}</h3>
                    <p>{{ project.description }}</p>
                    <div class="tech-stack">
                        <span v-for="tech in project.technologies" :key="tech" class="tech-tag">
                            {{ tech }}
                        </span>
                    </div>
                    <a v-if="project.link" :href="project.link" target="_blank" class="project-link">
                        View Project →
                    </a>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue'

const projects = ref([
    {
        id: 1,
        title: 'E-Commerce Platform',
        description: 'A full-featured online shopping platform with payment integration',
        technologies: ['Laravel', 'Vue.js', 'MySQL'],
        link: '#'
    },
    {
        id: 2,
        title: 'Task Management System',
        description: 'Collaborative task tracking application for teams',
        technologies: ['Laravel', 'Tailwind CSS', 'MySQL'],
        link: '#'
    },
    {
        id: 3,
        title: 'Blog CMS',
        description: 'Content management system with rich text editor and media library',
        technologies: ['Laravel', 'Bootstrap', 'PostgreSQL'],
        link: '#'
    }
])
</script>

<style scoped>
.projects-section {
    padding: 4rem 0;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
}

h2 {
    margin-bottom: 2rem;
    text-align: center;
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

.project-card {
    background: var(--secondary);
    border: 1px solid var(--tertiary);
    padding: 2rem;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    backdrop-filter: blur(10px);
}

.project-card h3 {
    font-size: 1.3rem;
    margin-bottom: 1rem;
}

.project-card p {
    margin-bottom: 1rem;
    flex: 1;
}

.tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 1rem;
}

.tech-tag {
    background: var(--tertiary);
    padding: 0.3rem 0.8rem;
    border-radius: 4px;
    font-size: 0.85rem;
    color: var(--secondary);
    border: none;
}

.project-link {
    color: var(--tertiary);
    text-decoration: none;
    font-weight: 500;
}

.project-link:hover {
    text-decoration: underline;
}
</style>
