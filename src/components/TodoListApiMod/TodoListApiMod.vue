<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        @addTodoItem="addOneItem" 
      />
      <TodoListInner 
        v-bind:propsdata="todoItems"
        @removeItem="removeOneItem"
        @toggleEvent="toggleOneItem" 
      />
      <TodoListFooter 
        @clearAll="clearAllItems"
      />
  </div>
</template>
<script setup>
import TodoListHeader from '@/components/TodoListApiMod/TodoListHeader.vue'
import TodoListInput from '@/components/TodoListApiMod/TodoListInput.vue'
import TodoListInner from '@/components/TodoListApiMod/TodoListInner.vue'
import TodoListFooter from '@/components/TodoListApiMod/TodoListFooter.vue'
import {ref, onMounted} from 'vue';

const todoItems = ref([]);
function addOneItem(todoItem){
  let obj = {completed: false, item: todoItem};
  localStorage.setItem(todoItem, JSON.stringify(obj));
  todoItems.value.push(obj);
}

function removeOneItem(todoItem, index){
  todoItems.value.splice(index,1);
  localStorage.removeItem(todoItem.item);
}

function toggleOneItem(todoItem, index){
  todoItems.value[index].completed = !todoItems.value[index].completed;
  localStorage.removeItem(todoItem.item);
  localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
}

function clearAllItems(){
  localStorage.clear();
  todoItems.value = [];
}

onMounted(() => {
  console.log("onMounted")
  if(localStorage.length > 0){
    for(var i = 0; i<localStorage.length; i++){
      if(localStorage.key(i) !== 'loglevel:webpack-dev-serve'){
        todoItems.value.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
      }
    }
  }
})
</script>
<style>
  
</style>