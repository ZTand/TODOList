<template>
  <transition-group name="list" tag="ul">
    <li v-for="(todoItem, index) in todoItems" :key="todoItem.unikey">
      <div class="itemContainer">
        <button class="changeBtn" @click="changeTodo(index, todoItem.data, true)">
          <i class="toggleBtn" :class="iconChoose[index]"></i>
        </button>
        <div class="item">
          <div class="itemText" :style="divStyle[index]">{{ todoItem.data }}</div>
          <form v-on:submit.prevent="() => changeTodo(index, todoItem.data, true)">
            <input
              class="itemEdit"
              type="text"
              ref="input"
              :style="inputStyle[index]"
              :value="todoItem.data"
              @input="(event) => changeTodo(index, event.target.value, false)"
            />
          </form>
        </div>
        <button class="removeBtn" @click="removeTodo(index)"><i class="far fa-trash-alt"></i></button>
      </div>
    </li>
  </transition-group>
</template>

<script>
export default {
  props: ['todoItems'],

  data() {
    return {
      iconChoose: [],
      divStyle: [],
      inputStyle: []
    }
  },
  created() {
    const parseData = JSON.parse(localStorage.getItem('todo'))
    if (parseData !== null) {
      for (let i = 0; i < parseData.length; i++) {
        this.iconChoose.push({
          far: true,
          'fa-edit': true,
          fas: false,
          'fa-check': false
        })
        this.divStyle.push({
          display: 'inline'
        })
        this.inputStyle.push({
          display: 'none'
        })
      }
    }
  },
  methods: {
    removeTodo(index) {
      this.$emit('removeTodo', index)
    },
    changeTodo(index, todoItem, b) {
      if (b) {
        this.iconChoose[index].far = !this.iconChoose[index].far
        this.iconChoose[index]['fa-edit'] = !this.iconChoose[index]['fa-edit']
        this.iconChoose[index].fas = !this.iconChoose[index].fas
        this.iconChoose[index]['fa-check'] = !this.iconChoose[index]['fa-check']
        this.divStyle[index].display === 'inline'
          ? (this.divStyle[index].display = 'none')
          : (this.divStyle[index].display = 'inline')
        this.inputStyle[index].display === 'inline'
          ? (this.inputStyle[index].display = 'none')
          : (this.inputStyle[index].display = 'inline')

        this.$nextTick(() => {
          this.$refs.input[index].focus()
        })
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
  transition: all 1s;
}
.list-enter {
  opacity: 0;
  transform: translateX(10px);
}
.list-leave-to {
  opacity: 0;
  transform: translateX(10px);
}
</style>