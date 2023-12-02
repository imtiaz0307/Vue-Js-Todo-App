<script setup>
import { ref, defineProps } from "vue";
import "./styles/modal.css"

let { todo, todos, isOpen, toggle } = defineProps(["todo", "todos", "isOpen", "toggle"])

const title = ref(todo.title)
const date = ref(todo.deadline.slice(0, 10).split("-").reverse().join("-"))
const time = ref(todo.deadline.slice(14, 19))
const priority = ref(todo.priority)

const updateHandler = () => {
    const _todos = [...todos]
    const currentTodo = _todos.splice(todo.id - 1, 1)[0]
    currentTodo.priority = priority.value;
    currentTodo.title = title.value;
    currentTodo.deadline = `${date.value.toString().split("-").reverse().join("-")} at ${time.value}PM`;

    console.log(currentTodo)
    _todos.splice(todo.id - 1, 0, currentTodo)

    todos = _todos
    localStorage.setItem("todos", JSON.stringify(todos))
    toggle()
}

</script>

<template>
    <div :class="{ modal_overlay: true, modal_overlay_visible: isOpen }">
        <div :class="{ modal_dialog: true, modal_dialog_visible: isOpen }">
            <div class="modal_header">
                <h4>Edit Todo</h4>
                <span style="cursor: pointer;" @click="toggle">x</span>
            </div>
            <div class="modal_body">
                <div class="input_container">
                    <label for="title">Title:</label>
                    <input id="title" type="text" placeholder="Todo Title" v-model="title">
                </div>
                <div class="input_container">
                    <label>Deadline:</label>
                    <div>
                        <input id="deadline" type="date" placeholder="Deadline" v-model="date">
                        <input id="deadline" type="time" placeholder="time" v-model="time">
                    </div>
                </div>
                <div class="input_container">
                    <label for="priority">Priority:</label>
                    <select id="priority" v-model="priority">
                        <option value="" disabled>--Select-Priority--</option>
                        <option value="HIGH">HIGH</option>
                        <option value="MEDIUM">MEDIUM</option>
                        <option value="LOW">LOW</option>
                    </select>
                </div>
            </div>
            <div class="modal_footer">
                <button @click="updateHandler">Update Todo</button>
            </div>
        </div>
    </div>
</template>