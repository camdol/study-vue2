<template>
  <div class="todolist">
      <TodoListHeader />
      <TodoListInput 
        @addTodoItem="addTodoItem" 
        @onChangeUser="onChangeUser"
        @onChangeItem="onChangeItem"
        :users="users" 
        :curUser="curUser"
        :items="items" 
        :curItem="curItem"
      />
      <TodoListInner v-for="item in items" :key="item"
        :item="item"
        :todoItems="_todoItems"
        :curUser="curUser"
        @removeItem="removeItem"
        @toggleEvent="toggleEvent" 
      />
      <TodoListFooter 
        @clearAll="clearAllItems"
      />
  </div>
</template>
<script setup>
import TodoListHeader from '@/components/TodoList/TodoListHeader.vue'
import TodoListInput from '@/components/TodoList/TodoListInput.vue'
import TodoListInner from '@/components/TodoList/TodoListInner.vue'
import TodoListFooter from '@/components/TodoList/TodoListFooter.vue'
import { ref, onMounted, computed } from 'vue';
const data = [
    {
        id: 1,
        user: '',
        todoItem: '할 일1',
        buyItem: '사고 싶은 것1',
        todoChecked: true,
        buyChecked: false,
    },
    {
        id: 2,
        user: '',
        todoItem: '할 일2',
        buyItem: '사고 싶은 것2',
        todoChecked: true,
        buyChecked: false,
    },
    {
        id: 3,
        user: '',
        todoItem: '할 일3',
        buyItem: '사고 싶은 것3',
        todoChecked: true,
        buyChecked: false,
    },
    {
        id: 4,
        user: '',
        todoItem: '할 일4',
        buyItem: '사고 싶은 것4',
        todoChecked: true,
        buyChecked: false,
    },
]
const todoItems = ref(data)
const users = ref([])
const items = ref([])
const curUser = ref('all')
const curItem = ref('')

setItems(data)
// item 종류
function setItems(data) {
    const _items = Object.keys(data[0])
        .filter((key) => key.includes("Item"))

    curItem.value = _items[0]
    items.value = _items
}

// 현재 사용자 변경
function onChangeUser(user) {
    curUser.value = user;
    filterData(); // 현재 사용자 해당 데이터 필터링
}
// 현재 사용자 변경
function onChangeItem(item) {
    curItem.value = item;
}
function addTodoItem(txt, user) {
    const _check = `${curItem.value.replace('Item', '')}Checked`;
    const obj = { id: `${txt}_${Math.random()*1000}`, [_check]: false, [curItem.value]:txt, user };
    setAddUser(user); // 사용자 추가
    todoItems.value.push(obj); // 데이터 넣기
}
function removeItem(id) {
    todoItems.value = todoItems.value.filter(item => item.id !== id);
    setUsers(); // 데이터 삭제되며 사용자 데이터 다시 셋팅
}
function toggleEvent(id) {
    todoItems.value = todoItems.value.map(todo => todo.id === id ? {...todo, done: !todo.done} : todo);
}
function clearAllItems() {
    todoItems.value = [];
    setUsers(); // 데이터 삭제되며 사용자 데이터 다시 셋팅
}
// user 추가
function setAddUser(user) {
    user !== '' && users.value.indexOf(user) === -1 && users.value.push(user);
    user === '' && users.value.indexOf('all') === -1 && users.value.push('all');
}
// user 배열 셋팅
function setUsers() {
    users.value = [];
    todoItems.value.map(item => {
        item.user === '' && users.value.indexOf('all') === -1 && users.value.push('all');
        item.user !== '' && users.value.indexOf(item.user) === -1 && users.value.push(item.user);
    });
}
// 사용자에 따라 데이터 필터링
function filterData() {
    return curUser.value === 'all' ? todoItems.value : todoItems.value.filter(todo => todo.user === curUser.value);
}

// 필터링된 데이터
const _todoItems = computed(() => filterData());

onMounted(() => setUsers());
</script>
<style scoped>
</style>