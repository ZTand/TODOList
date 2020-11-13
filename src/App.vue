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
  created() {
    const loadData = localStorage.getItem('todo')
    if (loadData !== null) {
      const parseData = JSON.parse(loadData)
      for (let data of parseData) {
        let item = {
          data: data.data,
          unikey: data.unikey
        }
        this.todoItems.push(item)
      }
    }
  },
  methods: {
    randomID() {
      return Math.random().toString(32)
    },
    addTodo(data) {
      const item = {
        data: data,
        unikey: this.randomID()
      }
      this.todoItems.push(item)
      this.localStorageUpdate()
    },
    removeTodo(index) {
      this.todoItems.splice(index, 1)
      this.localStorageUpdate()
    },
    changeTodo({ index, todoItem }) {
      let item = {
        data: todoItem,
        unikey: this.todoItems[index].unikey
      }
      this.todoItems.splice(index, 1, item)
      this.localStorageUpdate()
    },
    localStorageUpdate() {
      localStorage.clear()
      let ItemList = []
      let i = 0
      for (let item of this.todoItems) {
        let todo = {
          unikey: item.unikey,
          index: i++,
          data: item.data
        }
        ItemList.push(item)
      }
      localStorage.setItem('todo', JSON.stringify(ItemList))
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