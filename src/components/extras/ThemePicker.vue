<template>
    <div class="theme-picker">
        <div class="theme-info">
            <p>If you don't like the website palette, you can experiment and make your own theme.</p>
        </div>
        <div class="theme-controls">
            <label>
                <span>Primary</span>
                <input type="color" v-model="primary" @input="onInput('--primary', primary)" />
                <span class="colorcode">{{ primary }}</span>
            </label>

            <label>
                <span>Secondary</span>
                <input type="color" v-model="secondary" @input="onInput('--secondary', secondary)" />
                <span class="colorcode">{{ secondary }}</span>
            </label>

            <label>
                <span>Tertiary</span>
                <input type="color" v-model="tertiary" @input="onInput('--tertiary', tertiary)" />
                <span class="colorcode">{{ tertiary }}</span>
            </label>

            <label>
                <span>Text</span>
                <input type="color" v-model="text" @input="onInput('--text-base', text)" />
                <span class="colorcode">{{ text }}</span>
            </label>
            <button type="button" @click="resetTheme">
                Reset to default
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const STORAGE_KEY = 'themeColors'

const DEFAULTS = {
    primary: '#222831',
    secondary: '#31363f',
    tertiary: '#76abae',
    text: '#eeeeee',
}

const primary = ref(DEFAULTS.primary)
const secondary = ref(DEFAULTS.secondary)
const tertiary = ref(DEFAULTS.tertiary)
const text = ref(DEFAULTS.text)

const setCssVar = (name, value) => {
    document.documentElement.style.setProperty(name, value)
}

const applyAllToCss = () => {
    setCssVar('--primary', primary.value)
    setCssVar('--secondary', secondary.value)
    setCssVar('--tertiary', tertiary.value)
    setCssVar('--text-base', text.value)
}

const saveToStorage = () => {
    const data = {
        primary: primary.value,
        secondary: secondary.value,
        tertiary: tertiary.value,
        text: text.value,
    }
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data))
}

const onInput = (varName, valueRef) => {
    setCssVar(varName, valueRef)
    saveToStorage()
}

const resetTheme = () => {
    // reset refs
    primary.value = DEFAULTS.primary
    secondary.value = DEFAULTS.secondary
    tertiary.value = DEFAULTS.tertiary
    text.value = DEFAULTS.text

    // apply to CSS
    applyAllToCss()

    // clear storage
    localStorage.removeItem(STORAGE_KEY)
}

onMounted(() => {
    const saved = localStorage.getItem(STORAGE_KEY)
    if (saved) {
        try {
            const parsed = JSON.parse(saved)
            if (parsed.primary) primary.value = parsed.primary
            if (parsed.secondary) secondary.value = parsed.secondary
            if (parsed.tertiary) tertiary.value = parsed.tertiary
            if (parsed.text) text.value = parsed.text
        } catch (e) {
            // ignore, keep defaults
        }
    }
    applyAllToCss()
})
</script>

<style scoped>
.theme-picker {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 2rem;
    padding: 1rem;
    flex-wrap: wrap;
}

.theme-info {
    flex: 1;
    min-width: 250px;
}

.theme-controls {
    display: flex;
    align-items: center;
    gap: 1rem;
    flex-wrap: wrap;
}

label {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 0.8rem;
}

button {
    padding: 5px 10px;
    border: 1px solid black;
    border-radius: 15px;
    background-color: var(--secondary);
    color: var(--text-base);
}

.colorcode {
    font-family: monospace;
    font-size: 0.7rem;
}
</style>
