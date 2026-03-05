<template>
    <div class="game-view">
        <h1>Tic Tac Toe</h1>
        <TicTacToe />
    </div>
</template>

<script setup>
import TicTacToe from '@/components/games/TicTacToe.vue'
</script>

<style scoped>
.game-view {
    text-align: center;
}
</style>
