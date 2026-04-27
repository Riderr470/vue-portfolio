<template>
    <section class="skills-section">
        <div class="container">
            <h2>Skills</h2>

            <!-- Core Skills -->
            <div class="tag-group">
                <span class="group-label">Languages &amp; Frameworks</span>
                <div class="tag-row">
                    <span v-for="skill in coreSkills" :key="skill.name" class="tag tag--core">
                        <img :src="`https://cdn.simpleicons.org/${skill.icon}`" :alt="skill.name" class="tag-icon" />
                        {{ skill.name }}
                    </span>
                </div>
            </div>

            <!-- Additional Skills -->
            <div class="tag-group">
                <span class="group-label">Libraries &amp; Concepts</span>
                <div class="tag-row">
                    <span v-for="skill in additionalSkills" :key="skill" class="tag tag--secondary">
                        {{ skill }}
                    </span>
                </div>
            </div>

            <!-- Tools -->
            <div class="tag-group">
                <span class="group-label">Tools &amp; Environment</span>
                <div class="tag-row">
                    <span v-for="tool in tools" :key="tool.name" class="tag tag--tool">
                        <img :src="`https://cdn.simpleicons.org/${tool.icon}`" :alt="tool.name" class="tag-icon" />
                        {{ tool.name }}
                    </span>
                </div>
            </div>

        </div>
    </section>
</template>


<script setup>
import { ref } from 'vue'

const coreSkills = ref([
    { name: 'Laravel', icon: 'laravel' },
    { name: 'PHP', icon: 'php' },
    { name: 'Vue.js', icon: 'vuedotjs' },
    { name: 'JavaScript', icon: 'javascript' },
    { name: 'TypeScript', icon: 'typescript' },
    { name: 'MySQL', icon: 'mysql' },
    { name: 'HTML5', icon: 'html5' },
    { name: 'CSS3', icon: 'css' },
    { name: 'Livewire', icon: 'livewire' },
])

const additionalSkills = ref([
    'REST API',
    'Eloquent ORM',
    'Livewire',
    'Inertia.js',
    'Tailwind CSS',
    'Composer',
    'Node.js',
    'Redis',
    'Chart.js',
    'shadcn/ui',
    'MVC',
    'SOLID Principles',
])

const tools = ref([
    { name: 'VS Code', icon: 'visualstudio-code' },
    { name: 'MySQL', icon: 'mysql' },
    { name: 'Postman', icon: 'postman' },
    { name: 'GitHub', icon: 'github' },
    { name: 'Figma', icon: 'figma' },
    { name: 'npm', icon: 'npm' },
    // { name: 'Linux', icon: 'linux' },
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
}

.tag-group {
    margin-bottom: 1.25rem;
}

.group-label {
    display: block;
    font-size: 0.7rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--text-base);
    margin-bottom: 0.5rem;
}

.tag-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
}

.tag {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    padding: 0.4rem 0.8rem;
    border-radius: 4px;
    font-size: 0.875rem;
    font-weight: 600;
    line-height: 1;
    cursor: default;
    white-space: nowrap;
    transition: transform 120ms ease, box-shadow 120ms ease;
    border: 1px solid transparent;
}

.tag:hover {
    transform: translateY(-1px);
}

/* Core skill tags — Primary */
.tag--core {
    background: var(--primary);
    border-color: var(--primary);
    color: var(--text-base);
}

/* Additional / concept tags — Secondary */
.tag--secondary {
    background: var(--secondary);
    border-color: var(--secondary);
    color: var(--text-base);
}

.tag--secondary:hover {
    filter: brightness(1.1);
}

/* Tool tags — Tertiary */
.tag--tool {
    background: var(--tertiary);
    border-color: var(--tertiary);
    color: var(--text-base);
}

.tag--tool:hover {
    filter: brightness(1.2);
}

.tag-icon {
    width: 16px;
    height: 16px;
    object-fit: contain;
    display: inline-block;
    flex-shrink: 0;
    filter: brightness(0) invert(1);
}

.tag--core .tag-icon {
    filter: brightness(0) invert(1);
    opacity: 1;
}
</style>