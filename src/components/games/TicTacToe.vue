<template>
    <div class="tic-tac-toe">
        <div class="game-info">
            <h2 v-if="!winner && !isTie">Current Player: {{ currentPlayer }}</h2>
            <h2 v-if="winner" class="winner">🎉 Player {{ winner }} Wins!</h2>
            <h2 v-if="isTie" class="tie">It's a Tie!</h2>
        </div>

        <div class="board">
            <div v-for="(row, rowIndex) in board" :key="rowIndex" class="board-row">
                <button v-for="(cell, colIndex) in row" :key="colIndex" class="cell" :class="{ filled: cell }"
                    @click="playMove(rowIndex, colIndex)" :disabled="!!cell || !!winner || isTie">
                    {{ cell }}
                </button>
            </div>
        </div>

        <button @click="resetGame" class="reset-btn">Reset Game</button>
        <router-link to="/" class="back-btn">← Back to Games</router-link>
    </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const currentPlayer = ref('X')
const winner = ref(null)
const isTie = ref(false)

const board = reactive([
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
])

const playMove = (row, col) => {
    if (!board[row][col] && !winner.value && !isTie.value) {
        board[row][col] = currentPlayer.value

        if (checkWin()) {
            winner.value = currentPlayer.value
        } else if (checkTie()) {
            isTie.value = true
        } else {
            currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
        }
    }
}

const checkWin = () => {
    // Check rows
    for (let i = 0; i < 3; i++) {
        if (board[i][0] && board[i][0] === board[i][1] && board[i][1] === board[i][2]) {
            return true
        }
    }

    // Check columns
    for (let i = 0; i < 3; i++) {
        if (board[0][i] && board[0][i] === board[1][i] && board[1][i] === board[2][i]) {
            return true
        }
    }

    // Check diagonals
    if (board[0][0] && board[0][0] === board[1][1] && board[1][1] === board[2][2]) {
        return true
    }
    if (board[0][2] && board[0][2] === board[1][1] && board[1][1] === board[2][0]) {
        return true
    }

    return false
}

const checkTie = () => {
    for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
            if (!board[i][j]) {
                return false
            }
        }
    }
    return true
}

const resetGame = () => {
    for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
            board[i][j] = ''
        }
    }
    currentPlayer.value = 'X'
    winner.value = null
    isTie.value = false
}
</script>

<style scoped>
.tic-tac-toe {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
}

.game-info {
    margin-bottom: 2rem;
    min-height: 3rem;
}

.winner {
    color: #42b883;
}

.tie {
    color: #f39c12;
}

.board {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.board-row {
    display: flex;
    gap: 0.5rem;
}

.cell {
    width: 100px;
    height: 100px;
    font-size: 2.5rem;
    font-weight: bold;
    background: white;
    border: 3px solid #35495e;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
}

.cell:hover:not(:disabled) {
    background: #f0f0f0;
    transform: scale(1.05);
}

.cell:disabled {
    cursor: not-allowed;
}

.cell.filled {
    color: #42b883;
}

.reset-btn,
.back-btn {
    margin-top: 2rem;
    padding: 0.75rem 2rem;
    font-size: 1rem;
    border: 2px solid #42b883;
    border-radius: 6px;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
}

.reset-btn {
    background: #42b883;
    color: white;
}

.back-btn {
    margin-left: 1rem;
    background: white;
    color: #42b883;
}
</style>
