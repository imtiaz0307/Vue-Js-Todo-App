<script setup>
import { ref, reactive } from 'vue';
import "./styles/todos.css"
import Todoitem from './todoitem.vue';
import AddTodo from './add_todo.vue';

let id = 1

const priorities = ref(["HIGH", "MEDIUM", "LOW"])

const { todos } = reactive({ todos: JSON.parse(localStorage.getItem("todos")) ?? [] })

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
            <Todoitem v-if="todos.length > 0" v-for="(todo, index) in todos" :key="todo.id" :todo="todo"
                :priorities="priorities" :todos="todos" :index="index" />
            <div v-else class="empty_todos">No Todos To Show.</div>
        </div>
    </div>
</template>