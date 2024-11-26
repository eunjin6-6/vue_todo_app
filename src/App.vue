<script setup>
import { reactive, ref } from 'vue';
import Todo from './components/TodoItem.vue';

const todoText = ref('');

const addtodo = (e) =>{
  todoText.value = e.target.value;
  //빈칸없애기. 대상.trim();
  const todoTextLength = todoText.value.trim().length;
  
  if(todoTextLength > 0){
    todos.push({id: todoTextLength+1 , title: todoText.value, checked : false})  
  }

  todoText.value = '';
}

const todos = reactive([
  {id: 1, title: '웹 배우기', checked : false},
  {id: 2, title: '취업하기', checked : false}
])

const toggleCheckbox = (id, checked)=>{
  console.log(id, checked, todos.values);
  const idx = todos.findIndex(todo=> todo.id === id);
  todos[idx].checked = checked
}
</script>

<template>
 <div id="app" class="container">
  <h1>Vue Todo App</h1>

  <!-- 
  입력 내용 실시간 반영
  <BFormInput placeholder="할일을 입력하세요" v-model="todoText" />
  <Todo :todo="todoText" /> -->

  <!-- 입력 후 엔터 시 내용 추가 -->
  <BFormInput placeholder="할일을 입력하세요" @keyup.enter="addtodo" v-model="todoText"/>
  <Todo 
    v-for="todo in todos" 
    :key="todo.id" 
    :todo="todo" 
    @toggle-checkbox="toggleCheckbox"
  />

 </div>
</template>

<style scoped>
</style>