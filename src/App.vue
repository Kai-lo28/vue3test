<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

  import { reactive } from 'vue'
  import { ref } from 'vue'

  const counter = reactive({
    count: 0
  })

 // console.log(counter.count) // 0
  counter.count++

  const message = ref('Hello World!')
  
  //console.log(message.value) // "Hello World!"
  message.value = 'Changed'

  const count = ref(0)
  const state = reactive({
    count
  })
  
  console.log(state.count) // 0
  
  state.count = 1
  console.log(count.value) // 1

  const otherCount = ref(2)

  state.count = otherCount
  console.log(state.count) // 2
  // 原始 ref 现在已经和 state.count 失去联系
  console.log(count.value) // 1
  
  console.log(otherCount.value) // 2
  otherCount.value = 9
  console.log(state.count) // 9

  //Form Bindings
  const text = ref('')

  //List Rendering
  // give each todo a unique id
  let id = 0
  
  const newTodo = ref('')
  const todos = ref([
    { id: id++, text: 'Learn HTML' },
    { id: id++, text: 'Learn JavaScript' },
    { id: id++, text: 'Learn Vue' }
  ])
  
  function addTodo() {
    todos.value.push({ id: id++, text: newTodo.value})
    newTodo.value = ''
  }
  
  function removeTodo(todo) {
    todos.value = todos.value.filter((v) => v.id !== todo.id)
  }
</script>

<template>
  <h1>{{ message }}</h1>
  <p>count is: {{ counter.count }}</p>
  <h1>{{ message.split('').reverse().join('') }}</h1>
  <button @click="counter.count++">count</button>
  
  <br><hr>
  <!--Form Bindings-->
  <h1>Form Bindings</h1>
  <input v-model="text" placeholder="Type here">
  <p>{{ text }}</p>
  <br><hr>
  <!--List Rendering-->
  <h1>List Rendering</h1>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <!--
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
  -->
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
