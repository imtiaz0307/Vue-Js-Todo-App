<script setup>
import { ref, defineProps } from "vue";
import "./styles/modal.css"
import X from "../assets/icons/x_mark.vue";

let { todos, isOpen, toggle } = defineProps(["todos", "isOpen", "toggle"])

const title = ref("")
const date = ref("")
const time = ref("")
const priority = ref("")

const AddTodoHandler = () => {
    if (!title.value || !date.value || !time.value || !priority.value) return;
    const todo = {
        id: todos?.length + 1 ?? 1,
        title: title.value,
        priority: priority.value,
        deadline: `${date.value.toString().split("-").reverse().join("-")} at ${time.value}PM`
    }
    todos.push(todo)
    localStorage.setItem("todos", JSON.stringify(todos))

    title.value = ""
    date.value = ""
    time.value = ""
    priority.value = ""

    toggle()
}

</script>

<template>
    <div :class="{ modal_overlay: true, modal_overlay_visible: isOpen }">
        <div :class="{ modal_dialog: true, modal_dialog_visible: isOpen }">
            <div class="modal_header">
                <h4>Add New Todo</h4>
                <span style="cursor: pointer;" @click="toggle">
                    <X />
                </span>
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
                <button :disabled="!title || !date || !priority || !time" @click="AddTodoHandler">Add Todo</button>
            </div>
        </div>
    </div>
</template>