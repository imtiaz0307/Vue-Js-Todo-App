<script setup>
import { ref } from 'vue';

const navlinks = ref([
    { name: "Home", link: "/" },
    { name: "Todos", link: "/todos" },
    { name: "About", link: "/about" }
])
</script>

<template>
    <nav class="navbar">
        <div class="logo">Todoist</div>
        <ul class="nav__links">
            <li v-for="navlink in navlinks" :key="navlink.name">
                <a :href="navlink.link">{{ navlink.name }}</a>
            </li>
        </ul>
    </nav>
</template>

<style scoped>
.navbar {
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 5px #e9e9e9;
}

.logo {
    font-weight: 700;
    font-size: 1.5rem;
}

.nav__links {
    display: flex;
    gap: 4rem;
}

.nav__links li a {
    font-size: .7rem;
    font-weight: 900;
    color: #5925f0;
    text-transform: uppercase;
    opacity: .7;
}

.nav__links li a:hover {
    opacity: 1;
}

@media screen and (max-width:450px) {
    .navbar {
        flex-direction: column;
        align-items: center;
        gap: 2rem;
    }
}
</style>