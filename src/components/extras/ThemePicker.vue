<template>
    <div class="theme-picker">
        <label>
            Primary
            <input type="color" v-model="primary" @input="onInput('--primary', primary)" />
        </label>

        <label>
            Secondary
            <input type="color" v-model="secondary" @input="onInput('--secondary', secondary)" />
        </label>

        <label>
            Tertiary
            <input type="color" v-model="tertiary" @input="onInput('--tertiary', tertiary)" />
        </label>

        <label>
            Text Color
            <input type="color" v-model="text" @input="onInput('--text-base', text)" />
        </label>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const STORAGE_KEY = 'themeColors'

const primary = ref('#222831')
const secondary = ref('#31363f')
const tertiary = ref('#76abae')
const text = ref('#eeeeee')

const setCssVar = (name, value) => {
    document.documentElement.style.setProperty(name, value)
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

const applyAllToCss = () => {
    setCssVar('--primary', primary.value)
    setCssVar('--secondary', secondary.value)
    setCssVar('--tertiary', tertiary.value)
    setCssVar('--text-base', text.value)
}

const onInput = (varName, valueRef) => {
    setCssVar(varName, valueRef)
    saveToStorage()
}

onMounted(() => {
    // 1) load from localStorage if present
    const saved = localStorage.getItem(STORAGE_KEY)
    if (saved) {
        try {
            const parsed = JSON.parse(saved)
            if (parsed.primary) primary.value = parsed.primary
            if (parsed.secondary) secondary.value = parsed.secondary
            if (parsed.tertiary) tertiary.value = parsed.tertiary
            if (parsed.text) text.value = parsed.text
        } catch (e) {
            // ignore parse error, keep defaults
        }
    } else {
        // fallback: read from current CSS variables (optional)
        const styles = getComputedStyle(document.documentElement)
        primary.value = styles.getPropertyValue('--primary').trim() || primary.value
        secondary.value =
            styles.getPropertyValue('--secondary').trim() || secondary.value
        tertiary.value =
            styles.getPropertyValue('--tertiary').trim() || tertiary.value
        text.value = styles.getPropertyValue('--text-base').trim() || text.value
    }

    // 2) apply whatever values we ended up with
    applyAllToCss()
})
</script>
