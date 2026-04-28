<template>
    <Navbar />

    <section class="contact-section">
        <div class="container">

            <!-- Header -->
            <div class="contact-header" ref="headerRef">
                <span class="section-label">// contact</span>
                <h2>Get In Touch</h2>
                <p class="contact-subtext">
                    Have a project in mind or want to collaborate? My inbox is always open.
                </p>
            </div>

            <!-- Two-column layout -->
            <div class="contact-body">

                <!-- Left: contact links -->
                <div class="contact-links" ref="linksRef">
                    <div v-for="(link, i) in contactLinks" :key="link.label" class="contact-link-item"
                        :style="{ '--item-delay': `${i * 80}ms` }">
                        <a :href="link.href" target="_blank" rel="noopener noreferrer" class="contact-link">
                            <span class="link-icon" v-html="link.icon"></span>
                            <span class="link-body">
                                <span class="link-label">{{ link.label }}</span>
                                <span class="link-value">{{ link.value }}</span>
                            </span>
                            <span class="link-arrow">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)"
                                    stroke-width="2">
                                    <path d="M7 17L17 7M17 7H7M17 7v10" />
                                </svg>
                            </span>
                        </a>
                    </div>

                    <!-- Availability badge -->
                    <div class="availability">
                        <span class="avail-dot"></span>
                        <span>Available for freelance &amp; full-time opportunities</span>
                    </div>
                </div>

                <!-- Right: form -->
                <form class="contact-form" ref="formRef" @submit.prevent="handleSubmit" novalidate>
                    <!-- Terminal-style form header -->
                    <div class="form-topbar">
                        <span class="topbar-dot dot-red"></span>
                        <span class="topbar-dot dot-yellow"></span>
                        <span class="topbar-dot dot-green"></span>
                        <span class="topbar-title">new_message.txt</span>
                    </div>

                    <div class="form-body">
                        <div class="form-row">
                            <div class="field" :class="{ 'has-error': errors.name }">
                                <label for="contact-name">name<span class="required">*</span></label>
                                <input id="contact-name" v-model="form.name" type="text" placeholder="John Cena"
                                    autocomplete="name" @blur="validate('name')" />
                                <span v-if="errors.name" class="field-error">{{ errors.name }}</span>
                            </div>
                            <div class="field" :class="{ 'has-error': errors.email }">
                                <label for="contact-email">email<span class="required">*</span></label>
                                <input id="contact-email" v-model="form.email" type="email"
                                    placeholder="hello@example.com" autocomplete="email" @blur="validate('email')" />
                                <span v-if="errors.email" class="field-error">{{ errors.email }}</span>
                            </div>
                        </div>

                        <div class="field" :class="{ 'has-error': errors.subject }">
                            <label for="contact-subject">subject</label>
                            <input id="contact-subject" v-model="form.subject" type="text"
                                placeholder="Project collaboration" />
                        </div>

                        <div class="field" :class="{ 'has-error': errors.message }">
                            <label for="contact-message">message<span class="required">*</span></label>
                            <textarea id="contact-message" v-model="form.message" rows="5"
                                placeholder="Tell me about your project..." @blur="validate('message')"></textarea>
                            <span v-if="errors.message" class="field-error">{{ errors.message }}</span>
                        </div>

                        <button type="submit" class="submit-btn" :class="{ 'is-sent': sent, 'is-sending': sending }">
                            <span v-if="!sending && !sent" class="btn-content">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)"
                                    stroke-width="2">
                                    <path d="M22 2L11 13M22 2L15 22l-4-9-9-4 20-7z" />
                                </svg>
                                Send Message
                            </span>
                            <span v-else-if="sending" class="btn-content">
                                <svg class="spin" width="14" height="14" viewBox="0 0 24 24" fill="none"
                                    stroke="var(--tertiary)" stroke-width="2">
                                    <path d="M21 12a9 9 0 1 1-6.219-8.56" />
                                </svg>
                                Sending...
                            </span>
                            <span v-else class="btn-content">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)"
                                    stroke-width="2">
                                    <polyline points="20 6 9 17 4 12" />
                                </svg>
                                Sent!
                            </span>
                        </button>
                        <p v-if="submitError" class="submit-error">{{ submitError }}</p>
                    </div>
                </form>

            </div>
        </div>
    </section>
    <Footer />
</template>


<script setup>
import Footer from '@/components/partials/Footer.vue'
import Navbar from '@/components/partials/Navbar.vue'
import emailjs from '@emailjs/browser'
import { ref, reactive, onMounted } from 'vue'

const EMAILJS_SERVICE_ID = import.meta.env.VITE_EMAILJS_SERVICE_ID
const EMAILJS_TEMPLATE_ID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID
const EMAILJS_PUBLIC_KEY = import.meta.env.VITE_EMAILJS_PUBLIC_KEY

const headerRef = ref(null)
const linksRef = ref(null)
const formRef = ref(null)

const sending = ref(false)
const sent = ref(false)
const submitError = ref('')

const form = reactive({ name: '', email: '', subject: '', message: '' })
const errors = reactive({ name: '', email: '', message: '' })

const contactLinks = [
    {
        label: 'Email',
        value: 'riderr40@gmail.com',
        href: 'mailto:riderr40@gmail.com',
        icon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)" stroke-width="1.75">
              <rect x="2" y="4" width="20" height="16" rx="2"/>
              <path d="m22 7-10 7L2 7"/>
            </svg>`,
    },
    {
        label: 'GitHub',
        value: 'github.com/Riderr470',
        href: 'https://github.com/Riderr470',
        icon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)" stroke-width="1.75">
              <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
            </svg>`,
    },
    {
        label: 'LinkedIn',
        value: 'linkedin.com/in/ridan-rabab',
        href: 'https://www.linkedin.com/in/ridan-rabab/',
        icon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)" stroke-width="1.75">
              <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
              <rect x="2" y="9" width="4" height="12"/>
              <circle cx="4" cy="4" r="2"/>
            </svg>`,
    },
    {
        label: 'WhatsApp',
        value: '+880 1743757226',
        href: 'https://wa.me/8801743757226',
        icon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--tertiary)" stroke-width="1.75">
              <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/>
            </svg>`,
    },
]

function validate(field) {
    if (field === 'name') {
        errors.name = form.name.trim() ? '' : 'Name is required'
    }
    if (field === 'email') {
        if (!form.email.trim()) errors.email = 'Email is required'
        else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) errors.email = 'Enter a valid email'
        else errors.email = ''
    }
    if (field === 'message') {
        errors.message = form.message.trim() ? '' : 'Message is required'
    }
}

async function handleSubmit() {
    validate('name'); validate('email'); validate('message')
    if (errors.name || errors.email || errors.message) return

    sending.value = true

    try {
        await emailjs.send(
            EMAILJS_SERVICE_ID,
            EMAILJS_TEMPLATE_ID,
            {
                from_name: form.name,
                from_email: form.email,
                subject: form.subject || '(No subject)',
                message: form.message,
                reply_to: form.email,
            },
            EMAILJS_PUBLIC_KEY
        )

        sent.value = true
        form.name = form.email = form.subject = form.message = ''

    } catch (err) {
        console.error('EmailJS error:', err)
        submitError.value = 'Something went wrong. Please try again.'
    } finally {
        sending.value = false
    }
}

onMounted(() => {
    const observer = new IntersectionObserver(
        entries => entries.forEach(e => {
            if (e.isIntersecting) { e.target.classList.add('is-visible'); observer.unobserve(e.target) }
        }),
        { threshold: 0.1 }
    )
        ;[headerRef.value, linksRef.value, formRef.value].forEach(el => el && observer.observe(el))
})
</script>


<style scoped>
/* ── Section ── */
.contact-section {
    padding: clamp(3rem, 6vw, 5rem) 0;
}

.container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
}

/* ── Header ── */
.contact-header {
    text-align: center;
    margin-bottom: 3rem;
    opacity: 0;
    transform: translateY(14px);
    transition: opacity 400ms cubic-bezier(0.16, 1, 0.3, 1),
        transform 400ms cubic-bezier(0.16, 1, 0.3, 1);
}

.contact-header.is-visible {
    opacity: 1;
    transform: translateY(0);
}

.section-label {
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--primary);
    letter-spacing: 0.05em;
    display: block;
    margin-bottom: 0.5rem;
}

.contact-header h2 {
    font-size: clamp(1.6rem, 3vw, 2.2rem);
    font-weight: 700;
    color: var(--text-base);
    margin-bottom: 0.6rem;
}

.contact-subtext {
    font-size: 0.9rem;
    color: var(--text-base);
    max-width: 46ch;
    margin: 0 auto;
    line-height: 1.6;
}

/* ── Body layout ── */
.contact-body {
    display: grid;
    grid-template-columns: 1fr 1.45fr;
    gap: 2rem;
    align-items: start;
}

@media (max-width: 720px) {
    .contact-body {
        grid-template-columns: 1fr;
    }
}

/* ── Contact Links ── */
.contact-links {
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
    opacity: 0;
    transform: translateX(-14px);
    transition: opacity 420ms 80ms cubic-bezier(0.16, 1, 0.3, 1),
        transform 420ms 80ms cubic-bezier(0.16, 1, 0.3, 1);
}

.contact-links.is-visible {
    opacity: 1;
    transform: translateX(0);
}

.contact-link-item {
    opacity: 0;
    transform: translateX(-8px);
    transition: opacity 300ms var(--item-delay, 0ms) ease,
        transform 300ms var(--item-delay, 0ms) ease;
}

.contact-links.is-visible .contact-link-item {
    opacity: 1;
    transform: translateX(0);
}

.contact-link {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.65rem 0.85rem;
    border-radius: 6px;
    border: 1px solid var(--secondary);
    background: rgba(255, 255, 255, 0.03);
    text-decoration: none;
    transition: border-color 180ms ease,
        background 180ms ease,
        transform 180ms ease;
}

.contact-link:hover {
    border-color: var(--primary);
    background: rgba(255, 255, 255, 0.06);
    transform: translateX(3px);
}

.link-icon {
    color: var(--primary);
    display: flex;
    align-items: center;
    flex-shrink: 0;
    opacity: 0.8;
}

.link-body {
    display: flex;
    flex-direction: column;
    gap: 0.05rem;
    flex: 1;
    min-width: 0;
}

.link-label {
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    text-transform: uppercase;
    letter-spacing: 0.07em;
    color: var(--text-base);
    opacity: 0.6;
    line-height: 1;
}

.link-value {
    font-size: 0.82rem;
    font-weight: 500;
    color: var(--text-base);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.link-arrow {
    color: var(--text-base);
    opacity: 0.4;
    display: flex;
    align-items: center;
    transition: color 180ms ease, transform 180ms ease;
}

.contact-link:hover .link-arrow {
    color: var(--primary);
    transform: translate(2px, -2px);
}

/* Availability badge */
.availability {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-top: 0.75rem;
    padding: 0.4rem 0.7rem;
    border-radius: 4px;
    background: rgba(40, 200, 64, 0.1);
    border: 1px solid rgba(40, 200, 64, 0.3);
    font-size: 0.72rem;
    color: #28c840;
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    line-height: 1.4;
}

.avail-dot {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: #28c840;
    flex-shrink: 0;
    animation: pulse-dot 2.4s ease-in-out infinite;
}

@keyframes pulse-dot {

    0%,
    100% {
        box-shadow: 0 0 0 0 rgba(40, 200, 64, 0.4);
    }

    50% {
        box-shadow: 0 0 0 5px rgba(40, 200, 64, 0);
    }
}

/* ── Form ── */
.contact-form {
    border: 1px solid var(--secondary);
    border-radius: 8px;
    overflow: hidden;
    background: rgba(255, 255, 255, 0.02);
    opacity: 0;
    transform: translateY(14px);
    transition: opacity 420ms 140ms cubic-bezier(0.16, 1, 0.3, 1),
        transform 420ms 140ms cubic-bezier(0.16, 1, 0.3, 1);
}

.contact-form.is-visible {
    opacity: 1;
    transform: translateY(0);
}

/* Terminal topbar */
.form-topbar {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.55rem 0.85rem;
    background: var(--secondary);
    border-bottom: 1px solid var(--secondary);
}

.topbar-dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    flex-shrink: 0;
}

.dot-red {
    background: #ff5f57;
}

.dot-yellow {
    background: #ffbd2e;
}

.dot-green {
    background: #28c840;
}

.topbar-title {
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: var(--text-base);
    opacity: 0.5;
    margin-left: 0.4rem;
}

.form-body {
    padding: 1.25rem;
    display: flex;
    flex-direction: column;
    gap: 0.85rem;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.75rem;
}

@media (max-width: 480px) {
    .form-row {
        grid-template-columns: 1fr;
    }
}

/* Fields */
.field {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
}

.field label {
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    font-size: 0.67rem;
    text-transform: lowercase;
    letter-spacing: 0.04em;
    color: var(--text-base);
    opacity: 0.7;
}

.required {
    color: var(--primary);
    margin-left: 1px;
}

.field input,
.field textarea {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid var(--secondary);
    border-radius: 5px;
    padding: 0.5rem 0.7rem;
    font-size: 0.82rem;
    color: var(--text-base);
    line-height: 1.5;
    outline: none;
    transition: border-color 180ms ease, box-shadow 180ms ease;
    resize: vertical;
}

.field input::placeholder,
.field textarea::placeholder {
    color: var(--text-base);
    opacity: 0.3;
}

.field input:focus,
.field textarea:focus {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(var(--primary-rgb, 66, 184, 131), 0.15);
}

.has-error input,
.has-error textarea {
    border-color: #ff5f57;
}

.field-error {
    font-size: 0.68rem;
    color: #ff5f57;
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
}

/* Submit button */
.submit-btn {
    align-self: flex-start;
    display: inline-flex;
    align-items: center;
    padding: 0.5rem 1.1rem;
    border-radius: 5px;
    border: 1px solid var(--primary);
    background: transparent;
    color: var(--primary);
    font-family: 'Fira Code', 'Cascadia Code', 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 200ms ease;
}

.submit-error {
    font-size: 0.72rem;
    color: var(--color-error, #d163a7);
    margin-top: 0.35rem;
}

.submit-btn:hover {
    background: var(--primary);
    color: var(--text-base);
}

.submit-btn:active {
    transform: scale(0.97);
}

.submit-btn.is-sent {
    border-color: #28c840;
    color: #28c840;
}

.btn-content {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
}

@keyframes spin {
    to {
        transform: rotate(360deg);
    }
}

.spin {
    animation: spin 0.8s linear infinite;
}
</style>