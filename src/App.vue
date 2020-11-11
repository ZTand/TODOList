<template>
  <div id="app">
    <h1>TODOList</h1>
    <TodoInput @addTodo="addTodo"></TodoInput>
    <TodoList :todoItems="todoItems" @removeTodo="removeTodo" @changeTodo="changeTodo"></TodoList>
  </div>
</template>

<script>
import TodoInput from './components/TodoInput'
import TodoList from './components/TodoList'

export default {
  components: {
    TodoInput: TodoInput,
    TodoList: TodoList
  },
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    addTodo(item) {
      this.todoItems.push(item)
    },
    removeTodo(index) {
      this.todoItems.splice(index, 1)
    },
    changeTodo({ index, todoItem }) {
      this.todoItems.splice(index, 1, todoItem)
    }
  }
}
</script>

<style scoped>
html {
  box-sizing: border-box;
}
#app {
  height: 100vh;
  text-align: center;
  background-color: #aaaaaa;
}
h1 {
  padding-top: 2rem;
  letter-spacing: 2px;
  color: darkblue;
}
</style>