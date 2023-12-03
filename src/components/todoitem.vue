<script setup>
import MoreHorizontal from "../assets/icons/morehorizontal.vue"
import Clock from "../assets/icons/clock.vue"
import { defineProps, reactive, ref } from "vue";
import "./styles/todos.css"
import EditTodo from "./edit_todo.vue"
import DeleteTodo from "./delete_todo.vue";

let { todo, priorities, todos, index } = defineProps(["todo", "priorities", "todos", "index"])

// more
const showMore = ref(false)
const toggleShowMore = () => showMore.value = !showMore.value;

// dropdown
const showDropdown = ref(false)
const toggleDropdown = () => showDropdown.value = !showDropdown.value;

// priority handler
const prioritiyChangeHandler = (priority) => {
    const _todos = [...todos]
    const currentTodo = _todos.splice(index, 1)[0]
    currentTodo.priority = priority;

    _todos.splice(index, 0, currentTodo)

    todos = _todos
    localStorage.setItem("todos", JSON.stringify(todos))
}

// modal
const isEditOpen = ref(false)
const toggleEditModal = () => isEditOpen.value = !isEditOpen.value;
const isDeleteOpen = ref(false)
const toggleDeleteModal = () => isDeleteOpen.value = !isDeleteOpen.value;


// drag and sort
let { draggedItem } = reactive({ draggedItem: null })
let { draggedOverItem } = reactive({ draggedOverItem: null })

const sortHandler = () => {
    const _todos = [...todos]
    const currentTodo = _todos.splice(draggedItem, 1)[0]
    _todos.splice(draggedOverItem, 0, currentTodo)

    draggedOverItem = ""
    draggedItem = ""

    todos = _todos
    localStorage.setItem("todos", JSON.stringify(todos))
}

</script>

<template>
    <EditTodo :todo="todo" :todos="todos" :isOpen="isEditOpen" :toggle="toggleEditModal" :index="index" />
    <DeleteTodo :todo="todo" :todos="todos" :isOpen="isDeleteOpen" :toggle="toggleDeleteModal" :index="index" />
    <div class="todo_item" draggable="true" @dragstart="draggedItem = index" @dragenter="draggedOverItem = index"
        @dragend="sortHandler" @contextmenu="e => {
            e.preventDefault()
            toggleShowMore()
        }">
        <div class="todo_top">
            <h3>{{ todo.title }}</h3>
            <div class="top_menu" @click="toggleShowMore">
                <MoreHorizontal />
                <div :class="{ top_menu_menu: true, top_menu_menu_visible: showMore }">
                    <p @click="toggleEditModal">EDIT</p>
                    <p @click="toggleDeleteModal">DELETE</p>
                </div>
            </div>
        </div>
        <div class="todo_bottom">
            <p class="todo_deadline">
                <Clock />
                {{ todo.deadline }}
            </p>
            <div class="priority_dropdown" @click="toggleDropdown">
                <p :class="todo?.priority?.toLowerCase()">
                    {{ todo.priority }}
                </p>
                <div :class="{ priority_menu: true, priority_menu_visible: showDropdown }">
                    <p v-for=" priority  in   priorities  " :key="priority" @click="prioritiyChangeHandler(priority)">
                        {{ priority }}
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>