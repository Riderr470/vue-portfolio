<template>
    <section class="hero">
        <div class="hero-content-text">
            <div class="container-left">
                <h1>Hi, I'm Ridan Rabab Majumder</h1>
                <h2>Laravel Software Developer</h2>
                <p>Building web applications with Laravel, Vue.js, and modern technologies</p>
            </div>
        </div>
        <div class="hero-content-image">
            <div class="circle-wrapper">
                <div class="outer-circle">
                    <img src="/images/hero_bg.png" alt="Ridan Rabab Majumder">

                </div>
            </div>
        </div>
    </section>
</template>

<style>
.hero {
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    justify-content: space-evenly;
    min-height: 100vh;
    color: white;
    text-align: center;
}

.hero-content-text h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.hero-content-image {
    display: flex;
}

.hero-content h2 {
    font-size: 1.8rem;
    margin-bottom: 1rem;
    font-weight: 400;
}

.circle-wrapper {
    width: 300px;
    height: 300px;
    position: relative;
}

.outer-circle {
    position: relative;
    border-left: 2px solid var(--text-base);
    box-shadow: -5px 0 15px var(--tertiary);
    border-radius: 50%;
    width: 300px;
    height: 300px;
    overflow: hidden;
}

@property --angle {
    syntax: "<angle>";
    initial-value: 0deg;
    inherits: false;
}

.circle-wrapper::after {
    content: "";
    position: absolute;
    height: 110%;
    width: 110%;
    border-radius: 50%;
    background-image: conic-gradient(from var(--angle), var(--tertiary), var(--primary) 50%, var(--secondary), var(--tertiary));
    filter: blur(1.5rem);
    opacity: 0.5;
    top: 50%;
    left: 50%;
    translate: -50% -50%;
    padding: 10px;
    z-index: -1;
    animation: 6s spin linear infinite;
}

.outer-circle img {
    position: absolute;
    bottom: -70%;
    transform: translateX(-50%);
    max-width: 150%;
    background: radial-gradient(circle at center, var(--primary) 35%, var(--tertiary) 80%);
}

.hero-content p {
    font-size: 1.2rem;
    opacity: 0.9;
}

@keyframes spin {
    from {
        --angle: 0deg;
    }

    to {
        --angle: 360deg;
    }
}
</style>