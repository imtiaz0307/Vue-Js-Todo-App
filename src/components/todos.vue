<script setup>
import { ref } from 'vue';
import "./styles/todos.css"
import Todoitem from './todoitem.vue';
import AddTodo from './add_todo.vue';

let id = 1

const priorities = ref(["HIGH", "MEDIUM", "LOW"])

const todos = ref([
    {
        id: id++,
        title: "Go To Gym",
        deadline: "12-12-2023 at 03:00PM",
        priority: priorities.value[0]
    },
    {
        id: id++,
        title: "Parhle Bhai",
        deadline: "12-12-2023 at 03:00PM",
        priority: priorities.value[1]
    },
    {
        id: id++,
        title: "Code in Vue JS",
        deadline: "12-12-2023 at 03:00PM",
        priority: priorities.value[2]
    },
])

const showAddModal = ref(false)
const toggleAddModal = () => showAddModal.value = !showAddModal.value

</script>

<template>
    <AddTodo :todos="todos" :isOpen="showAddModal" :toggle="toggleAddModal" />
    <div class="card">
        <div class="card_header">
            <h2>Todos</h2>
            <button @click="toggleAddModal">Add New</button>
        </div>
        <div class="card_body">
            <Todoitem v-for="todo in todos" :key="todo.id" :todo="todo" :priorities="priorities" :todos="todos" />
        </div>
    </div>
</template>