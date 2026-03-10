<template>
    <div class="games-page">
        <Navbar />

        <div class="games-container">
            <ThemePicker />
            <h1>Mini Games Collection</h1>
            <div class="games-grid">
                <router-link to="/games/tic-tac-toe" class="game-card">
                    <h2>Tic Tac Toe</h2>
                    <p>Classic 3x3 game for two players</p>
                </router-link>
            </div>
        </div>

        <Footer />
    </div>
</template>

<script setup>
import Navbar from '@/components/partials/Navbar.vue'
import Footer from '@/components/partials/Footer.vue'
import ThemePicker from '@/components/extras/ThemePicker.vue';
</script>

<style scoped>
.games-page {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

.games-container {
    flex: 1;
    max-width: 1200px;
    margin: 0 auto;
    padding: 6rem 2rem 2rem;
}

.games-container h1 {
    margin-bottom: 2rem;
}

.games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1.5rem;
}

.game-card {
    border: 2px solid #42b883;
    border-radius: 8px;
    padding: 1.5rem;
    text-decoration: none;
    color: inherit;
    transition: transform 0.2s;
}

.game-card:hover {
    transform: translateY(-5px);
}
</style>
