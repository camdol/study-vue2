<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        v-on:addTodoItem="addOneItem" 
      />
      <TodoListInner 
        v-bind:propsdata="todoItems"
        v-bind:propsname="todoNames"
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
      todoItems: [],
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
      let obj = {completed: false, id: uuid, name: name, item: todoItem};
      localStorage.setItem(obj.id, JSON.stringify(obj));
      this.todoItems.push(obj);
      console.log(this.todoItems[2])
    },
    changeTodo: function(event) {
      //const asisSelect = this.selected1;
      // 변경 적용
      this.selected1 = event.target.value
      const selectData = this.propsdata.filter( item => item.name === this.selected1)
      return selectData
    },
    removeOneItem: function(todoItem, index){
      this.todoItems.splice(index, 1);
      localStorage.removeItem(todoItem.id);
    },
    toggleOneItem: function(todoItem, index){
      this.todoItems[index].completed = !this.todoItems[index].completed;
      // localStorage.removeItem(todoItem.item);
      // localStorage.setItem(todoItem.id, JSON.stringify(todoItem))
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