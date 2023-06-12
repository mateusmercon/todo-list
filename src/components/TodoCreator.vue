<script setup>
import { reactive, ref } from "vue";
import TodoButton from "./TodoButton.vue";

const emit = defineEmits(["create-todo"]);

const todoState = reactive({
  todo: "",
  invalid: null,
  errMsg: "",
});

const createTodo = () => {
  todoState.invalid = null;

  if (todoState.todo !== "") {
    emit('create-todo', todoState.todo);
    todoState.todo = ""
    return
  }

  todoState.invalid = true
  todoState.errMsg = "The to-do cannot be empty! :/"

};

const handleKeyPress = (event) => {
  event.preventDefault()
  createTodo()
};

</script>

<template>
  <div class="input-wrap" :class="{'input-err' : todoState.invalid}">
    <input 
      @keydown.enter="handleKeyPress" 
      type="text" 
      placeholder="Add your task..." 
      v-model="todoState.todo" 
    />
    <TodoButton @click="createTodo"/>
  </div>
  <p v-show="todoState.invalid" class="err-msg">
    {{ todoState.errMsg }}
  </p>
</template>




<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #415fb0;

  &.input-err {
    border-color: rgb(184, 37, 0);
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
  color: rgb(145, 30, 2);
}
</style>