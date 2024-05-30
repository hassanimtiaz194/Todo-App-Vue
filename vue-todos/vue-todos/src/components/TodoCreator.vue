<script setup>
import { ref, reactive, defineEmits } from 'vue';
import TodoButton from './TodoButton.vue';
const emit = defineEmits(["create-todo"]);
// ref is use to make our data reactive
// const todo = ref("");
// another way to make data reactive
const todoState = reactive({
    todo: "",
    invalid: null,
    errMsg : "",
});
const createTodo = () => {
    todoState.invalid = null;
    todoState.errMsg = "";
    if (todoState.todo.trim() === '') {
        todoState.invalid = true;
        todoState.errMsg = "Todo value cannot be empty.";
        return;
    }
    emit('create-todo', todoState.todo);
    todoState.todo = "";
};
</script>
<template>
    <div>
        <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
            <input type="text" v-model="todoState.todo" /> <!-- v-model="todoState.todo" -->
            <!-- <TodoButton @click="createTodo">Create</TodoButton> -->
            <TodoButton @click="createTodo" />
        </div>
    </div>
    <!-- v-if dont insert elemnt to dom -->
    <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->
    <!-- v-show insert elemnt to dom just changes css display to none  this is preffered-->
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
    <!--     <p>{{ todoState.todo }}</p> -->
</template>
<style lang="scss" scoped>
.input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41B080;
    &.input-err {
        border-color: red;
    }
    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }
    input {
        width: 100%;
        padding: 8px 6px;
        border: none;
        &:focus {
            outline: none;
        }
    }
}
.err-msg {
    margin-top: 6px;
    font-size: 12px;
    text-align: center;
    color: red;
}
</style>