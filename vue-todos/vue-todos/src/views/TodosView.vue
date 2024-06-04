<script setup>
import { Icon } from "@iconify/vue";
import { ref, watch, computed } from 'vue';
import { uid } from 'uid';
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from '../components/TodoItem.vue';
const todoList = ref([]);

// watch if todoList get updated deep property watches data inside todoList must be set true
watch(todoList, () => {
  setTodoListLocalStorage();
}, { deep: true })

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem('todoList'));
  if (savedTodoList) todoList.value = savedTodoList;
}

// automatically track reactive deps
const todosCompleted =  computed (() => {
  return todoList.value.every((todo) => todo.isCompleted );
})

// each time this page execute this fucntion will execute
fetchTodoList();

const setTodoListLocalStorage = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value));
}

const createTodo = (todo) => {
  console.log(todo);
  console.log(uid());
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
}
console.log(todoList);
const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
}
const todoEditClicked = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
}
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter(todo => todo.id !== todoId)
}
const updateTodo = (todoValue, todoPos) => {
  todoList.value[todoPos].todo = todoValue;
}
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length !== 0">
      <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @toggle-complete="toggleTodoComplete"
        @edit-todo="todoEditClicked" @delete-todo="deleteTodo" @update-todo="updateTodo" />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <p v-if="todosCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

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
</style>