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
</script>

<template>
  <h1>{{ message }}</h1>
  <p>count is: {{ counter.count }}</p>
  <h1>{{ message.split('').reverse().join('') }}</h1>
  <button @click="counter.count++">
count
</button>
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
