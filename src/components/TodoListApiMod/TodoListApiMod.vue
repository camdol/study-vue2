<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        @addTodoItem="addOneItem" 
      />
      <TodoListInner 
        v-bind:propsdata="todoChgItems"
        v-bind:propsname="todoNames"
        @removeItem="removeOneItem"
        @toggleEvent="toggleOneItem" 
        @changeEvent="changeTodoItem"
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
import {ref, onMounted, computed} from 'vue';

const todoItems = ref([])
const todoChgItems = ref([])

const todoNames = computed(() => {
  return [...new Set(todoItems.value.map((el) => el.name))];
})

function addOneItem(name, todoItem){
  let uuid = localStorage.length + 1
  const obj = {completed: false, id: uuid, name: name, item: todoItem}
  localStorage.setItem(obj.id, JSON.stringify(obj))
  todoItems.value.push(obj)
  todoChgItems.value = todoItems.value
}

function changeTodoItem(event) {
  let selectItem = event.target.value
  if(selectItem === 'all') {
    return todoChgItems.value = todoItems.value
  }
  todoChgItems.value = todoItems.value.filter( item => item.name === selectItem)
  return todoChgItems.value
}

function removeOneItem(todoItem, index){
  todoItems.value.splice(index, 1)
  localStorage.removeItem(todoItem.id)
  todoChgItems.value = todoItems.value
}

function toggleOneItem(todoItem, index){
  todoItems.value[index].completed = !todoItems.value[index].completed
  localStorage.removeItem(todoItem.id)
  localStorage.setItem(todoItem.id, JSON.stringify(todoItem))
}

function clearAllItems(){
  localStorage.clear()
  todoItems.value = []
  todoChgItems.value = []
}

onMounted(() => {
  console.log("onMounted")
  if(localStorage.length > 0){
    for(let i = 0; i<localStorage.length; i++){
      if(localStorage.key(i) !== 'loglevel:webpack-dev-serve'){
        todoItems.value.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        todoChgItems.value = todoItems.value
      }
    }
  }
})
</script>
<style scoped>
  
</style>