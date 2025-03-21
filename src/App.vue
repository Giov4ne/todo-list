<template>
  <div id="form-todo">
    <h1 id="title">Todo App</h1>
    <div id="input-container">
      <input type="text" id="input-todo">
      <button id="add-btn">
        <i class="fa fa-plus"></i>
      </button>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  
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

  #form-todo{
    margin: 38px 12px 12px 12px;
  }

  #title{
    color: var(--text-color);
    margin-bottom: 16px;
    font-size: 35px;
  }

  #input-container{
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
  }

  #input-todo{
    width: 320px;
    padding: 5px 12px;
    font-size: 18px;
    outline: none;
    border: none;
    border-radius: 5px 0 0 5px;
    background-color: #474747;
    color: var(--text-color);
    &:hover{
      background-color: #3b3b3b;
    }
  }

  #add-btn{
    padding: 5px 9px;
    font-size: 18px;
    background-color: #ffb951;
    outline: none;
    border: none;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    &:hover{
      background-color: rgb(255, 162, 76);
    }
  }
</style>