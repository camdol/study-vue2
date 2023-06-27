<template>
  <div class="todo-inner">
    <h3>{{ content }}</h3>
    <ul>
      <li 
        v-for="todoItem in props.todoItems"
        :key="todoItem.id"
        class="shadow">
        <button 
          type="button"
          :class="{ checkBtnCompleted: todoItem[_checked] }"
          v-on:click="toggleEvent(todoItem.id, content)"
        >
          <span class="checkBtn">
            <i class="fas fa-check"></i>
          </span>
          {{ todoItem[content] }} <span class="user">{{ todoItem.user }}</span>
        </button>
        
        <button 
          type="button"
          class="removeBtn" 
          @click="removeTodo(todoItem.id, content)">
          <i class="fas fa-trash-alt"></i>
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue'

const props = defineProps(['todoItems', 'curUser', "content"])
const emit = defineEmits(['removeItem', 'toggleEvent'])

function removeTodo(id, content) {
  emit('removeItem', id, content)
}
function toggleEvent(id, content) {
  emit('toggleEvent', id, content)
}
const _checked = computed(() => `${props.content.replace('Content', '')}Checked`);
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
  min-height: 30px;
  height: 30px;
  margin: 0.5rem 0 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
  line-height: 30px;
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
.checkBtnCompleted .checkBtn {color: #b3adad;}
.textCompleted {
  color: #b3adad;
  text-decoration: line-through;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
</style>