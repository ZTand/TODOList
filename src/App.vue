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
      for (let i = 0; i < parseData.length; i++) {
        let item = new Object()
        item.data = parseData[i].data
        item.unikey = parseData[i].unikey
        this.todoItems.push(item)
      }
    }
  },
  methods: {
    randomID() {
      return Math.random().toString(32)
    },
    addTodo(data) {
      let item = new Object()
      item.data = data
      item.unikey = this.randomID()
      this.todoItems.push(item)
      this.localStorageUpdate()
    },
    removeTodo(index) {
      this.todoItems.splice(index, 1)
      this.localStorageUpdate()
    },
    changeTodo({ index, todoItem, b }) {
      let item = new Object()
      item.data = todoItem
      item.unikey = this.todoItems[index].unikey
      this.todoItems.splice(index, 1, item)
      this.localStorageUpdate()
    },
    localStorageUpdate() {
      localStorage.clear()
      let ItemList = new Array()
      for (let i = 0; i < this.todoItems.length; i++) {
        let item = new Object()
        item.unikey = this.todoItems[i].unikey
        item.index = i
        item.data = this.todoItems[i].data
        ItemList.push(item)
      }
      const Data = JSON.stringify(ItemList)
      localStorage.setItem('todo', Data)
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