<template>
  <div>
      <h2>230518-스터디 Todolist</h2>
      <TodoListApi />
      <TodoListTemplate />
  </div>
</template>

<script>
import TodoListApi from './components/TodoListApi/TodoListApi.vue'
import TodoListTemplate from './components/TodoList/TodoListTemplate.vue'
export default {
  name: 'App',
  components: {
    TodoListApi,
    TodoListTemplate
  }
}
</script>

<style>
body,p,h1,h2,h3,h4,h5,h6,ul,ol,li,dl,dt,dd,table,th,td,form,fieldset,legend,input,textarea,button,select{margin:0;padding:0}
img,fieldset{border:0}
em,address,i{font-style:normal;}
a{text-decoration:none;}
table{border-collapse:collapse;}
ul li, 
ol li {
  list-style:none;
}
button {
  border:none;
  background:transparent;
  cursor: pointer;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
