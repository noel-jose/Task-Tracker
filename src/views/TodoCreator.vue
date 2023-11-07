        
<script setup>
    import { ref,reactive } from 'vue';
    const todo =  ref("testing")
    // to access value in ref in a script  we use todo.value
    // in the ref method we can only work with primitive data types
    const todoState = reactive({
        todo : "Testing"
    })
    // to access value of reactive element in the script we use
    // todoState.todo
    // in the reactive method we can work with not only primitive data
</script>
<template>
    <div class="input-wrap">
        <input type="text" name="" id="" v-model="todoState.todo">
        <button>Create</button>
    </div>
    <p>{{todoState.todo}}</p>
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