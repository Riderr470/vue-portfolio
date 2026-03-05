<template>
    <nav ref="navbar" class="navbar">
        <div class="nav-container">
            <router-link to="/" class="logo">Ridan Rabab Majumder</router-link>

            <div class="nav-links">
                <router-link to="/">Home</router-link>
                <router-link to="/about">About</router-link>
                <router-link to="/contact">Contact</router-link>
                <router-link to="/games">Fun</router-link>
            </div>
        </div>
    </nav>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const navbar = ref(null)

onMounted(() => {
    const handleScroll = () => {
        if (!navbar.value) return
        const scrolled = window.scrollY > 0
        navbar.value.classList.toggle('scrolled', scrolled)
    }

    window.addEventListener('scroll', handleScroll)
    // also check on load
    handleScroll()

    return () => {
        window.removeEventListener('scroll', handleScroll)
    }
})
</script>

<style scoped>
.navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding: 1rem 0;
    background: transparent;
    backdrop-filter: none;
    transition: all 0.3s ease;
}

/* State when scrolled */
.navbar.scrolled {
    background: transparent;
    /* dark semi‑opaque glass */
    backdrop-filter: blur(10px);
}

.nav-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: var(--text-base);
    text-decoration: none;
}

.nav-links {
    display: flex;
    gap: 2rem;
    align-items: center;
}

.nav-links a {
    color: var(--text-base);
    text-decoration: none;
    /* No opacity change on hover */
    transition: none;
}
</style>
