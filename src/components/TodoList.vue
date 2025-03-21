<template>
    <FormTodo/>
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
import FormTodo from './FormTodo.vue';

    export default{
        name: 'TodoList',
        components: {
            FormTodo
        }
    }
</script>

<style>
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