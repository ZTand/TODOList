<template>
  <div>
    <form>
      <input
        id="input"
        :class="[isEmpty ? 'HalfOpac' : 'FullOpac']"
        ref="input"
        type="text"
        v-model="todoItem"
        placeholder="할 일 입력"
      /><!--
    --><button @click="addTodo"><i class="fas fa-plus" aria-hidden="true"></i></button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItem: ''
    }
  },
  mounted() {
    this.$refs.input.focus()
  },
  methods: {
    addTodo() {
      if (this.todoItem !== '') {
        this.$emit('addTodo', this.todoItem)
        this.todoItem = ''
      }
    }
  },
  computed: {
    isEmpty() {
      return this.todoItem === ''
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