<template>
  <div class="clearAllContainer">
      <span class="clearAllBtn" v-on:click="clearTodo">
        Clear All
      </span>
  </div>
</template>

<script setup>
import { defineEmits } from 'vue'

const emit = defineEmits(['clearAll'])
function clearTodo() {
  emit('clearAll');
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
  cursor: pointer;
}
</style>