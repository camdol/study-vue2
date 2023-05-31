<template>
  <div class="input">
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model="newName"
        ref="name"
        placeholder="Name"
      >
    </div>
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model="newTodoItem"
        v-on:keyup.enter="addTodo"
        placeholder="To do list"
      >
      <button
        class="addContainer"
        v-on:click="addTodo"
      >
        <i class="fas fa-plus addBtn" aria-hidden="true"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import {ref, defineEmits} from 'vue';

const emit = defineEmits(['addTodoItem'])

const newTodoItem = ref("")
const newName = ref("")
const name = ref()

function addTodo() {
  if(newTodoItem.value !== "" && newName.value !==''){
    // this.$emit('이벤트 이름', 인자1, 인자2, ...);
    emit('addTodoItem', newName.value, newTodoItem.value)
    clearInput();
    name.value.focus();
  }
}
function clearInput() {
  newTodoItem.value=""
  newName.value=""
}
</script>
<style scoped>
.input {
  display:flex;
  max-width:500px;
  margin:0 auto;
}
input:focus {
  outline: none;
}
.input__box {
  width:120px;
  background: white;
  height: 48px;
  line-height: 48px;
  border-radius: 5px;
}
.input__box + .input__box {
  width:calc(100% - 120px);
  margin-left:10px;
}
.input__box + .input__box input {
  width:calc(100% - 3rem);
}
.input__box input {
  width:100%;
  padding:2px 15px;
  border-style: none;
  box-sizing:border-box;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #62EAC6, #32CEE6);
  display: block;
  width: 3rem;
  height: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>