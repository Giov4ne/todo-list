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
  <main>
    <ul id="list-container">
      <li>
        <label for="todo-1">
          <input type="checkbox" id="todo-1" class="check-todo" checked>
          <del>Academia</del>
        </label>
        <div>
          <span class="todo-options" title="Excluir">❌</span>
          <span class="todo-options" title="Editar">✏️</span>
        </div>
      </li>
      <li>
        <label for="todo-2">
          <input type="checkbox" id="todo-2" class="check-todo">
          Trabalhar
        </label>
        <div>
          <span class="todo-options" title="Excluir">❌</span>
          <span class="todo-options" title="Editar">✏️</span>
        </div>
      </li>
      <li>
        <label for="todo-3">
          <input type="checkbox" id="todo-3" class="check-todo">
          Estudar
        </label>
        <div>
          <span class="todo-options" title="Excluir">❌</span>
          <span class="todo-options" title="Editar">✏️</span>
        </div>
      </li>
    </ul>
  </main>
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
    cursor: default;
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
      background-color: #ffa24c;
    }
  }




  #list-container{
    list-style: none;
    color: var(--text-color);
    font-size: 18px;
    padding-top: 8px;
    cursor: default;
  }

  #list-container li{
    border-bottom: 1px solid #ffb951;
    padding: 8px 12px;
    margin-bottom: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 600px;
  }

  #list-container li label{
    display: flex;
    align-items: center;
    margin-right: 8px;
  }

  #list-container li label .check-todo{
    margin-right: 6px;
    min-width: 18px;
    min-height: 18px;
    cursor: pointer;
    &:checked{
      accent-color: #ffb951;
    }
  }

  #list-container li .todo-options{
    margin-left: 2px;
    font-size: 20px;
    cursor: pointer;
  }

  del{
    text-decoration: line-through;
    text-decoration-thickness: 2px;
  }
</style>