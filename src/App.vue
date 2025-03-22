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
    --main-background-color: #0e0e0e;
    --second-background-color: #474747;
    --third-background-color: #000000b6;
    --error-message-color: #E8363B;
    --main-hover-color: #ffa24c;
    --color1: #ffb951;
    --color2: #686868;
    --color3: #3b3b3b;
    --color4: #000;
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
    background-color: var(--main-background-color);
  }
</style>