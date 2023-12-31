<script setup>
import { Icon } from "@iconify/vue";
import {ref, watch,computed} from "vue";
import {uid} from "uid"
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from "../components/TodoItem.vue";

const todoList = ref([]);

watch(todoList,()=>{
  setTodoItems()
},{
  deep:true
})

const allTodosCompleted = computed(()=>{
  return todoList.value.every((todo)=> todo.isCompleted )
})

const fetchTodoItems = () => {
  const todoItems = JSON.parse(localStorage.getItem('todoList'));
  if(todoItems){
    todoList.value = todoItems
  }
}

fetchTodoItems();

const setTodoItems = () => {
  localStorage.setItem('todoList',JSON.stringify(todoList.value))
}

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo:todo, 
    isCompleted:null,
    isEditing:null,
  })
}

const toggleTodoComplete = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted
}

const toggleTodoEditing = (index) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing
}

const updateTodo = (index,value) => {
  todoList.value[index].todo = value
}

const deleteTodo = (id) => {
  todoList.value = todoList.value.filter((todo) => todo.id != id)
}
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo"/>
    <ul class="todo-list" v-if='todoList.length > 0'>
      <TodoItem v-for="(todo,index) in todoList" :todo="todo" :index="index" :key="todo.id" @toggle-complete="toggleTodoComplete" @toggle-editing="toggleTodoEditing" @todo-data-update="updateTodo" @delete-todo="deleteTodo"/>
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <p class="todos-msg" v-if="allTodosCompleted && todoList.length > 0">
      <Icon icon="noto-v1:fireworks"  />
      <span>You have completed all the todos</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main{
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width:100%;
  margin: 0 auto;
  padding: 40px 16px;

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}

h1{
  margin-bottom: 16px;
  text-align: center;
}
</style>
