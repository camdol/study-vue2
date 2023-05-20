<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        v-on:addTodoItem="addOneItem" 
      />
      <TodoListInner 
        v-bind:propsdata="todoItems"
        v-on:removeItem="removeOneItem"
        v-on:toggleEvent="toggleOneItem" 
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
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index){
      this.todoItems.splice(index,1);
      localStorage.removeItem(todoItem.item);
    },
    toggleOneItem: function(todoItem, index){
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
    },
    clearAllItems: function() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function() {
    if(localStorage.length > 0){
      for(var i = 0; i<localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-serve'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
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