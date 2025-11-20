<script setup>
import { ref, computed } from 'vue'
import WatchExample from './components/WatchExample.vue';
const counter = ref({ count: 10 })
const message = ref('Hello World!')

const classFlag = ref(false);
const titleClass = ref('title-red');
const nameOfColor = ref('red')
const inputText = ref('')
const greeting = ref('greeting from parent')

function increment() {
  counter.value.count++;
}

function toggleClass()
{
    classFlag.value = !classFlag.value;
    titleClass.value =  classFlag.value ? 'title-green': 'title-red';
    nameOfColor.value = classFlag.value ? 'green' : 'red';
}

//
// give each todo a unique id
let id = 0
const hideCompleted = ref(false)
const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML', done: false },
  { id: id++, text: 'Learn JavaScript',done: true },
  { id: id++, text: 'Learn Vue',done: false }
])

const filteredTodos = computed(() => {
  // return filtered todos based on
  // `todos.value` & `hideCompleted.value`
  if ( hideCompleted.value)
    return todos.value.filter(x => !x.done)

    return todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
//

</script>

<template>
  <h1>You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>

  <div>
    <h1>{{ message }}</h1>
    <p>Count is: {{ counter.count }}</p>
    <button @click="increment">Count is: {{ counter.count }}</button>
    <button @click="toggleClass">Toggle class</button>
  </div>

  <div>
    <h1 :class="titleClass">Make me {{nameOfColor}}</h1>
  </div>

  <div>
    <h3>Input binding with model:</h3>
    <input v-model="inputText" placeholder="Type here">
    <p>"{{ inputText }}"</p>
  </div>

  <div>
    <h3>Conditional rendering:</h3>
    <h1 v-if="classFlag">Vue is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
  </div>

  <div>
    <h3>List rendering and computed property:</h3>
     <form @submit.prevent="addTodo">

      <input v-model="newTodo" required placeholder="new todo">
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
  </div>

  <WatchExample :msg="greeting" />
</template>

<style scoped>

.title-red {
  color: red;
}

.title-green {
  color: green;
}

.done {
  text-decoration: line-through;
}

</style>
