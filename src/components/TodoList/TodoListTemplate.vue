<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        v-on:addTodoItem="addOneItem" 
      />
      <TodoListInner 
        v-bind:propsdata="todoChgItems"
        v-bind:propsname="todoNames"
        v-on:removeItem="removeOneItem"
        v-on:toggleEvent="toggleOneItem"
        v-on:changeEvent="changeTodoItem"
      />
      <TodoListFooter 
        v-on:clearAll="clearAllItems"
      />
  </div>
</template>
<script>
import TodoListHeader from '@/components/TodoList/TodoListHeader.vue'
import TodoListInput from '@/components/TodoList/TodoListInput.vue'
import TodoListInner from '@/components/TodoList/TodoListInner.vue'
import TodoListFooter from '@/components/TodoList/TodoListFooter.vue'
export default {
  name:'TodoList Home',
  components : {
    TodoListHeader,
    TodoListInput,
    TodoListInner,
    TodoListFooter
  },
  data () {
    return {
      todoItems: [],
      todoChgItems: [],
    }
  },
  computed: {
    todoNames(){
      return [...new Set(this.todoItems.map((el) => el.name))];
    }
  },
  methods: {
    addOneItem: function(name, todoItem) {
      let uuid = localStorage.length + 1
      let obj = {completed: false, id: uuid, name: name, item: todoItem}
      localStorage.setItem(obj.id, JSON.stringify(obj))
      this.todoItems.push(obj)
      this.todoChgItems = this.todoItems
    },
    changeTodoItem: function(event) {
      let selectItem = event.target.value
      if(selectItem === 'all') {
        return this.todoChgItems = this.todoItems
      }
      this.todoChgItems = this.todoItems.filter( item => item.name === selectItem)
      return this.todoChgItems
    },
    removeOneItem: function(todoItem, index){
      this.todoItems.splice(index, 1)
      localStorage.removeItem(todoItem.id)
      this.todoChgItems = this.todoItems
    },
    toggleOneItem: function(todoItem, index){
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.id);
      localStorage.setItem(todoItem.id, JSON.stringify(todoItem))
    },
    clearAllItems: function() {
      localStorage.clear()
      this.todoItems = []
      this.todoChgItems = []
    }
  },
  created: function() {
    if(localStorage.length > 0){
      for(var i = 0; i<localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-serve'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          this.todoChgItems = this.todoItems
        }
      }
    }
  }
}
</script>
<style>
body {
  text-align: center;
  background-color: #F6F6F6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>