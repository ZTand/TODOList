<template>
  <div>
    <input
      id="input"
      :class="[isEmpty ? 'HalfOpac' : 'FullOpac']"
      type="text"
      v-model="TodoItem"
      @keypress="checkEnter()"
      placeholder="할 일 입력"
    /><!--
    --><button @click="addTodo"><i class="fas fa-plus" aria-hidden="true"></i></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      TodoItem: ''
    }
  },
  mounted() {
    document.getElementById('input').focus()
  },
  methods: {
    addTodo() {
      if (this.TodoItem !== '') {
        this.$emit('addTodo', this.TodoItem)
        this.TodoItem = ''
      }
    },
    checkEnter() {
      if (event.keyCode == 13) {
        this.addTodo()
      }
    }
  },
  computed: {
    isEmpty() {
      return this.TodoItem === ''
    }
  }
}
</script>

<style scoped>
input {
  background-color: #dddddd;
  display: inline-block;
  width: 75%;
  height: 40px;
  padding: 0 0 0 16px;
  border: none;
}
button {
  width: 15%;
  height: 40px;
  padding: 0;
  border: none;
  background-color: #6c708b;
}
.HalfOpac {
  opacity: 0.5;
}
.FullOpac {
  opacity: 1;
}
</style>