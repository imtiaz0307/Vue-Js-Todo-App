<script setup>
import { defineProps } from 'vue';

const { toggleTheme, isDark } = defineProps(["toggleTheme", "isDark"])

</script>

<template>
    <nav class="navbar">
        <div class="logo">Todoist</div>
        <ul class="nav__links">->
            <button @click="toggleTheme">
                {{ isDark ? "Switch To Light" : "Switch To Dark" }}
            </button>
        </ul>
    </nav>
</template>

<style scoped>
.navbar {
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 5px var(--box-shadow-color);
    background-color: var(--color-bg);
}

.logo {
    font-weight: 700;
    font-size: 1.5rem;
    color: var(--color-text);
}

.nav__links {
    display: flex;
    gap: 4rem;
    align-items: center;
}

.nav__links button {
    width: 170px;
}

.nav__links li a {
    font-size: .7rem;
    font-weight: 900;
    color: var(--color-primary);
    text-transform: uppercase;
    opacity: .7;
}

.nav__links li a:hover {
    opacity: 1;
}

@media screen and (max-width:450px) {
    .navbar {
        padding: 1rem;
    }

    .nav__links button {
        widows: 150px;
    }

    /* .navbar {
        flex-direction: column;
        align-items: center;
        gap: 2rem;
    }

    .nav__links {
        gap: 1rem;
    }

    .nav__links button {
        display: none;
    } */
}
</style>