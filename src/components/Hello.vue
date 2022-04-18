<script setup>
import {reactive,ref ,onMounted,computed,watch} from 'vue'

const counter = reactive({ count: 10 })
const message = ref('Hello Hien!')
const titleClass = ref("title")
const count = ref(0)
function increment(){
    count.value++
}
const text = ref('')
const awesome = ref(true)
function toggle(){
    awesome.value = !awesome.value
}


let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)

const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn Vue' }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

const p = ref(null)
onMounted(() => {
  p.value.textContent = 'mounted!'
})

const todoId = ref(1)
const todoData = ref(null)

async function fetchData() {
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
}

fetchData()

watch(todoId, fetchData)



import ChildComp from './icons/ChildComp.vue'

const greeting = ref('Hello from parent')
const childMsg = ref('No child msg yet')


const msg = ref('from parent')
</script>

<template>
<p>Count is: {{ counter.count }}</p>
  <h1>{{ message }}</h1>

  <h1 :class="titleClass">Make me red</h1>
  <button @click="increment">count is: {{ count }}</button>
  <input v-model="text" placeholder="Type here">
  <p>{{text}}</p>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome</h1>
  <h1 v-else>Oh no :( </h1>


  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>


<p ref="p">hello</p>



<p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>


<ChildComp />

<ChildComp :msg="greeting" />

<ChildComp @response="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>


<ChildComp>Message: {{ msg }}</ChildComp>
</template>