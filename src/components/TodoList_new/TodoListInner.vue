<template>
  <div class="todo-inner">
    <h3>{{ item }}</h3>
    <ul>
       <template v-for="todoItem in props.todoItems" :key="todoItem.id">
        <li v-if="todoItem[item]">
          <button 
            type="button"
            :class="{ checkBtnCompleted: todoItem.checked }"
            @click="toggleComplete(todoItem.id, item)"
          >
            <span
              class="checkBtn" 
            >
              <i class="fas fa-check"></i>
            </span>
            {{ todoItem[item] }} <span class="user">{{ todoItem.user }}</span>
          </button>
          <button 
            type="button"
            class="editBtn" 
            @click="editItem(todoItem.id, todoItem[item])">
            <i class="fas fa-pencil-alt"></i>
          </button>
          <button 
            type="button"
            class="removeBtn" 
            @click="removeTodo(todoItem.id, item)">
            <i class="fas fa-trash-alt"></i>
          </button>
        </li>
      </template>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['todoItems', 'curUser', 'item'])
const emit = defineEmits(['removeItem', 'toggleEvent', 'editItem'])

function editItem(id, item) {
 emit('editItem', id, item)
}
function removeTodo(id, item) {
  emit('removeItem', id, item)
}
function toggleComplete(id, item) {
  emit('toggleEvent', id, item)
}
</script>
<style scoped>
.no-data {display:none}
.todo-inner {max-width:500px;margin:20px auto;}
h3 {text-align:left;}
ul + h3{margin-top:50px;}
ul {
  margin-top: 0;
  padding-left: 0;
  text-align: left;
  list-style-type: none;
}
li {
  display: flex;
  gap:10px;
  min-height: 30px;
  height: 35px;
  margin: 0.5rem 0 0;
  padding: 0 0.9rem;
  background: white;
}
li button {
    font-size: 15px;
}
.user {
    font-size: 13px;
    color: #999;
}
.checkBtn {
  color: #62acde;
  margin-right: 5px;
  line-height: 45px;
}
.checkBtnCompleted,
.checkBtnCompleted .checkBtn {color: #b3adad;text-decoration:line-through;}
.editBtn {
  margin-left: auto;
  color: #505050;
}
.removeBtn {
  color: #de4343;
}
</style>