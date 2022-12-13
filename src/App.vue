<template id="app">
  <todo-app></todo-app>
</template>

<script>

import TodoApp from "./components/TodoApp.vue"
export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
#app{
  background: #d4d4d4;
  width: 100%;
  height: 100vh;
}
</style>
