<template>
  <TodoList/>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100..900;1,100..900&display=swap');

  :root{
    --text-color: #fff;
  }

  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: "Roboto", serif;
  }

  body, #form-todo{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  body{
    background-color: #0e0e0e;
  }
</style>