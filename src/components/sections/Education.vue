<template>
    <section class="education-section">
        <div class="container">
            <h2>Education</h2>

            <div class="edu-timeline">
                <div v-for="edu in education" :key="edu.id" class="edu-entry">
                    <!-- Left: year badge -->
                    <div class="edu-year">
                        <span>{{ edu.year.split(' - ')[0] }}</span>
                        <span class="year-sep">↓</span>
                        <span>{{ edu.year.split(' - ')[1] }}</span>
                    </div>

                    <!-- Connector -->
                    <div class="edu-connector">
                        <div class="connector-dot"></div>
                        <div class="connector-line"></div>
                    </div>

                    <!-- Right: content card -->
                    <div class="edu-card">
                        <div class="edu-card-header">
                            <span class="edu-badge">{{ edu.badge }}</span>
                            <span class="edu-institution">{{ edu.institution }}</span>
                        </div>
                        <h3 class="edu-degree">{{ edu.degree }}</h3>
                        <p class="edu-desc">{{ edu.description }}</p>
                    </div>
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
        badge: 'B.Sc',
        degree: 'Computer Science',
        institution: 'American International University Bangladesh',
        year: '2019 - 2024',
        description: 'Focused on web development and software engineering'
    },
    {
        id: 2,
        badge: 'HSC',
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
    margin-bottom: 2.5rem;
    text-align: center;
}

/* ── Timeline Layout ── */
.edu-timeline {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 100%;
    margin: 0 auto;
}

.edu-entry {
    display: grid;
    grid-template-columns: 72px 28px 1fr;
    gap: 0 0.75rem;
    align-items: start;
}

/* ── Year Column ── */
.edu-year {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    padding-top: 0.15rem;
    gap: 0.05rem;
    font-size: 0.7rem;
    font-weight: 500;
    color: var(--text-base);
    opacity: 0.8;
    line-height: 1.3;
    min-width: 0;
}

.year-sep {
    font-size: 0.6rem;
    line-height: 1;
}

/* ── Connector Column ── */
.edu-connector {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 0.35rem;
}

.connector-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--primary);
    box-shadow: 0 0 0 2px var(--secondary);
    flex-shrink: 0;
}

.connector-line {
    width: 2px;
    flex: 1;
    min-height: 100%;
    background: linear-gradient(to bottom,
            var(--primary) 0%,
            var(--secondary) 100%);
    margin-top: 4px;
}

/* Hide line on last entry */
.edu-entry:last-child .connector-line {
    display: none;
}

/* ── Card ── */
.edu-card {
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid var(--secondary);
    border-radius: 6px;
    padding: 1.5rem;
    margin-bottom: 2rem;
}

.edu-card-header {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 0.75rem;
    flex-wrap: wrap;
}

.edu-badge {
    font-size: 0.65rem;
    font-weight: 600;
    padding: 0.1rem 0.4rem;
    border-radius: 3px;
    background: var(--primary);
    color: var(--text-base);
    letter-spacing: 0.04em;
    text-transform: uppercase;
}

.edu-institution {
    font-size: 0.9rem;
    color: var(--text-base);
    opacity: 0.7;
    font-weight: 400;
    line-height: 1.2;
}

.edu-degree {
    font-size: 1.25rem;
    color: var(--tertiary);
    margin-bottom: 0.5rem;
    line-height: 1.3;
}

.edu-desc {
    font-size: 0.95rem;
    color: var(--text-base);
    opacity: 0.8;
    line-height: 1.5;
    max-width: 100%;
    margin: 0;
}

/* ── Responsive ── */
@media (max-width: 480px) {
    .edu-timeline {
        max-width: 100%;
    }

    .edu-entry {
        grid-template-columns: 60px 24px 1fr;
        gap: 0 0.5rem;
    }

    .edu-year {
        font-size: 0.65rem;
    }
}
</style>