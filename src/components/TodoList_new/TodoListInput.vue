<template>
  
  <div class="input">
    <select @change="onChangeItem">
      <option 
        v-for="item in props.items" 
        :key="item" 
        :value="item"
      >
      {{ item }}
      </option>
    </select>
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model.trim="user"
        placeholder="이름 입력"
      >
    </div>
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model.trim="newTodoItem"
        v-on:keyup.enter="addTodo"
      >
      <button
        class="addContainer"
        @click="addTodo"
      >
        <i class="fas fa-plus addBtn" aria-hidden="true"></i>
      </button>
    </div>
  </div>
  <div class="select">
    <select @change="onChangeUser">
      <option 
        v-for="user in props.users" 
        :key="user" 
        :value="user"
      >
        {{ user }}
      </option>
    </select>
  </div>
</template>

<script setup>
import { ref, defineEmits, defineProps } from 'vue';
const props = defineProps(["users", "curUser", "items", "curItem"]);
const emit = defineEmits(["addTodoItem", "onChangeUser", "onChangeItem"])
const newTodoItem = ref("")
const user = ref()

function onChangeUser(e) {
  emit("onChangeUser", e.target.value);
}

function onChangeItem(e) {
  console.log(e.target.value)
  emit("onChangeItem", e.target.value);
}

function addTodo() {
  if(newTodoItem.value !== ""){
    // this.$emit('이벤트 이름', 인자1, 인자2, ...);
    emit('addTodoItem', newTodoItem.value, user.value)
    clearInput()
  } else {
    alert("내용 입력해주세요");
  }
}
function clearInput() {
  newTodoItem.value=""
}
</script>
<style scoped>
.select {
  max-width:500px;
  margin:10px auto;
  text-align:right;
}
select {
  border: 1px solid #bfbfbf;
  border-radius: 4px;
  padding: .8em .6em;
  background: white;
  transition: background-color .5s;
  width:120px;
  height: 48px;
}
select + .input__box {margin-left:10px;}
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
  border:1px solid #bfbfbf;
}
.input__box + .input__box {
  width:calc(100% - 240px);
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