<script setup>
import { defineProps } from "vue";
import "./styles/modal.css"
import X from "../assets/icons/x_mark.vue";

let { todo, todos, isOpen, toggle } = defineProps(["todo", "todos", "isOpen", "toggle"])

const deleteHandler = () => {
    const _todos = [...todos]
    const filtered = _todos.filter(item => item.id !== todo.id)
    todos.value = filtered.filter(item => item !== null);
    localStorage.setItem("todos", JSON.stringify(todos))

    toggle()
}

</script>

<template>
    <div :class="{ modal_overlay: true, modal_overlay_visible: isOpen }">
        <div :class="{ modal_dialog: true, modal_dialog_visible: isOpen }">
            <div class="modal_header">
                <h4>Delete Todo</h4>
                <span style="cursor: pointer;" @click="toggle">
                    <X />
                </span>
            </div>
            <div class="modal_body">
                <p>Are you sure, you want to delete this todo?</p>
            </div>
            <div class="modal_footer">
                <button @click="toggle">Cancel</button>
                <button @click="deleteHandler">Delete Todo</button>
            </div>
        </div>
    </div>
</template>