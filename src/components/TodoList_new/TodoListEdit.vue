<template>
  <div v-if="props.modelValue" class="modal">
    <div class="dimm"></div>
    
    <div class="modal-body">
        <input type="text">
        <button @click="eidtTodo">
            수정
        </button>
        <button @click="closePopup">
            취소
        </button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
//const props = defineProps(["curEditId", "curEditItem", "ModelValue"])
const props = defineProps({
  modelValue: {
    Type: String,
    required: true
    }
});
const emit = defineEmits(['update:modelValue'])
//const editTodoItem = ref("")

function closePopup() {
  emit('update:modelValue')
}
</script>
<style scoped>
/* Modal */
.modal,
.dimm {
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  top: 0;
}
.dimm {
  opacity: 0.5;
  background-color: black;
}
.modal-body {
  position: relative;
  top:calc(50% - 3.125rem);
  max-width: 25rem;
  margin:0 auto;
  padding: 1.25rem;
  background-color: white;
  min-height: 6.25rem;
  z-index: 10;
  opacity: 1;
}
</style>