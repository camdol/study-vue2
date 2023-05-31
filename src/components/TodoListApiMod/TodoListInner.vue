<template>
  <div class="todo-inner">
    <div class="select">
      <select @change="changeTodo($event)">
        <option disabled value="">이름을 선택하세요</option>
        <option value="all">전체</option>
        <option v-for="name in props.propsname" :key="name" :value="name">{{ name }}</option>
      </select>
    </div>
    <ul>
      <li 
        v-for="(todoItem, index) in props.propsdata"
        :key="index"
        class="shadow">
        <button 
          type="button"
          :class="{'checkBtnCompleted': !todoItem.completed}"
          v-on:click="toggleComplete(todoItem, index)"
        >
          <span
            class="checkBtn" 
          >
            <i class="fas fa-check"></i>
          </span>
          {{ todoItem.name }} :
          {{ todoItem.item }}
        </button>
        
        <button 
          type="button"
          class="removeBtn" 
          v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['propsdata', 'propsname'])
const emit = defineEmits(['removeItem', 'toggleEvent', 'changeEvent'])

function changeTodo($event) {
  emit('changeEvent', $event);
}
function removeTodo(todoItem, index){
  console.log('todoItem', todoItem)
  emit('removeItem', todoItem, index)
}
function toggleComplete(todoItem, index){
  emit('toggleEvent', todoItem, index)
}

</script>
<style scoped>
.select {
  max-width:500px;
  margin:10px auto;
  text-align:right;
}
select {
  border: 1px solid #f4f4f4;
  border-radius: 4px;
  padding: .8em .6em;
  margin-top: 10px;
  background: white;
  transition: background-color .5s
}

ul {
  max-width:500px;
  margin:0 auto;
  margin-top: 0;
  padding-left: 0;
  text-align: left;
  list-style-type: none;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  margin: 0.5rem 0 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
  line-height: 50px;
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