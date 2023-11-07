        
<script setup>
    import { ref,reactive,defineEmits } from 'vue';
    const emit = defineEmits(['create-todo'])
    const todo =  ref("")
    // to access value in ref in a script  we use todo.value
    // in the ref method we can only work with primitive data types
    // const todoState = reactive({
    //     todo : "Testing"
    // })
    // to access value of reactive element in the script we use
    // todoState.todo
    // in the reactive method we can work with not only primitive data

    const createTodo = () => {
        emit('create-todo',todo.value)
    }
</script>
<template>
    <div class="input-wrap">
        <input type="text" name="" id="" v-model="todo">
        <button @click="createTodo">Create</button>
    </div>
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

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

  button {
    padding: 8px 16px;
    border: none;
  }
}
</style>