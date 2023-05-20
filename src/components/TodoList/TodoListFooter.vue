<template>
  <div 
    class="clearAllContainer">
    <button
      type="button"
      class="clearAllBtn shadow"
      v-on:click="clearTodo">
      Clear All
    </button>
  </div>
</template>
<script>
export default {
  methods:{
    clearTodo: function () {
      this.$emit('clearAll');
    }
  }
}
</script>
<style>
.clearAllContainer {
  margin-top:20px;
  line-height: 50px;
  text-align:center;
}
.clearAllBtn {
  display:inline-block;
  width: 8.5rem;
  height: 50px;
  background:#fff;
  border-radius: 5px;
  line-height: 50px;
  color: #e20303;
}
</style>