<template>
  <div class="input">
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model="newName"
        placeholder="name"
      >
    </div>
    <div class="input__box shadow">
      <input 
        type="text" 
        v-model="newTodoItem"
        placeholder="todo list"
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
<script>
export default {
  data: function () {
    return {
      newTodoItem:"",
      newName:"",
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem !== '' && this.newName !==''){
        // this.$emit('이벤트 이름', 인자1, 인자2, ...);
        console.log("name", this.newName)
        console.log("newTodoItem", this.newTodoItem)
        this.$emit('addTodoItem', this.newName, this.newTodoItem)
        this.clearInput();
      }
    },
    clearInput: function(){
      this.newTodoItem = '';
      this.newName = '';
    }
  }
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