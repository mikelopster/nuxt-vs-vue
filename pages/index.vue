<script setup>
const BASE_URL = 'https://64ffc48218c34dee0cd3ef15.mockapi.io'

const statuses = ['Pending', 'Doing', 'Done']
const todoText = ref('')
const isLoading = ref(true)
const todos = ref([])

const loadTodo = async () => {
  isLoading.value = true
  const { data } = useFetch(`${BASE_URL}/todos`, {
    lazy: true
  })
  console.log(data)
  todos.value = data.value
  isLoading.value = false
}

const addTodo = async () => {
  try {
    isLoading.value = true
    const todoData = {
      name: todoText.value,
      status: 'Pending'
    }
    await useFetch(`${BASE_URL}/todos`, {
      method: 'post',
      body: todoData
    })
    await loadTodo()
  } catch (error) {
    console.log('error', error)
  }
  isLoading.value = false
}

const deleteTodo = async (id) => {
  try {
    isLoading.value = true
    await useFetch(`${BASE_URL}/todos/${id}`, {
      method: 'delete'
    })
    await loadTodo()
  } catch (error) {

  }

  isLoading.value = false
}

// load in state setup
await loadTodo()
</script>

<template>
  <div>
    <h1>Todo List</h1>
    <div>
      <input type="text" v-model="todoText">
      <button @click="addTodo">Add</button>
    </div>
    <ul v-if="!isLoading">
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.name }}
        status :
        <select v-model="todo.status">
          <option v-for="status in statuses" :key="status" :value="status">
            {{ status }}
          </option>
        </select>

        <nuxt-link
          :to="`/todo/${todo.id}`">
          <button>Edit</button>
        </nuxt-link>
        <button @click="deleteTodo(todo.id)">DELETE</button>
      </li>
    </ul>
    <div v-else>
      Loading
    </div>
  </div>
</template>

