<template>
  <transition-group name="list" tag="ul">
    <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.unikey">
      <div class="itemContainer">
        <button class="changeBtn" @click="changeTodo(index, todoItem.data, true)">
          <i class="toggleBtn far fa-edit"></i>
        </button>
        <div class="item">
          <div class="itemText" style="display: inline">{{ todoItem.data }}</div>
          <input
            class="itemEdit"
            type="text"
            style="display: none"
            :value="todoItem.data"
            @input="(event) => changeTodo(index, event.target.value, false)"
            @keypress="checkEnter(index, todoItem.data)"
          />
        </div>
        <button class="removeBtn" @click="removeTodo(index)"><i class="far fa-trash-alt"></i></button>
      </div>
    </li>
  </transition-group>
</template>

<script>
export default {
  props: ['todoItems'],
  methods: {
    checkEnter(index, todoItem) {
      if (event.keyCode === 13) {
        this.changeTodo(index, todoItem, true)
      }
    },
    removeTodo(index) {
      this.$emit('removeTodo', index)
    },
    changeTodo(index, todoItem, b) {
      if (b) {
        const btn = document.getElementsByClassName('toggleBtn').item(index)
        if (btn.className === 'toggleBtn far fa-edit') {
          btn.classList.remove('far')
          btn.classList.remove('fa-edit')
          btn.classList.add('fas')
          btn.classList.add('fa-check')
        } else {
          btn.classList.remove('fas')
          btn.classList.remove('fa-check')
          btn.classList.add('far')
          btn.classList.add('fa-edit')
        }
        const text = document.getElementsByClassName('itemText').item(index)
        if (text.style.display == 'none') {
          text.style.display = 'inline'
        } else {
          text.style.display = 'none'
        }
        const edit = document.getElementsByClassName('itemEdit').item(index)
        if (edit.style.display == 'none') {
          edit.style.display = 'inline'
        } else {
          edit.style.display = 'none'
        }
        edit.focus()
      }
      this.$emit('changeTodo', { index, todoItem, b })
    }
  }
}
</script>

<style scoped>
ul {
  padding-left: 0;
}
li {
  width: auto;
  list-style-type: none;
  background: #ffffff;
  margin: 4px 8px;
}
.itemContainer {
  display: flex;
  justify-content: space-between;
}
button {
  width: 35px;
  height: 35px;
}
.changeBtn {
  color: #3333ff;
}
.removeBtn {
  color: #de4343;
}
.item {
  width: 100%;
  height: 35px;
  line-height: 35px;
  padding-left: 16px;
  text-align: left;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.7s;
}
.list-enter {
  opacity: 0;
  transform: translateX(10px);
}
.list-leave-to {
  opacity: 0;
  transform: translateX(3px);
}
</style>