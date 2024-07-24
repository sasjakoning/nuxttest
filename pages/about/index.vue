<template>
    <div class="about">
        <h1>Todo List</h1>
        <ul class="list">
            <li v-for="(todo, index) in todos" :key="index">
                <ListItem @remove="removeTodo(index)">
                    {{ todo }}
                </ListItem>
            </li>
            <div class="list-add-wrapper">
                <input 
                class="list-add"
                v-model="newTodo" 
                @keyup.enter="addTodo" 
                placeholder="Add a new todo">
            </div>
        </ul>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const todos = ref([])
const newTodo = ref('')

onMounted(() => {
    console.log(localStorage)
    const savedTodos = localStorage.getItem('todos')
    if (savedTodos) {
        todos.value = JSON.parse(savedTodos)
    }
})

const addTodo = () => {
    if (newTodo.value.trim() !== '') {
        console.log('Adding new todo:', newTodo.value)
        todos.value.push(newTodo.value) // Add the todo first
        localStorage.setItem('todos', JSON.stringify(todos.value)) // Then save the updated list to localStorage
        newTodo.value = '' // Clear the input field
    }
}

const removeTodo = (index) => {
    todos.value.splice(index, 1)
    localStorage.setItem('todos', JSON.stringify(todos.value))
}
</script>

<style lang="scss">
@import 'about';
</style>