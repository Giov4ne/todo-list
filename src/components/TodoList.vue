<template>
    <FormTodo @add-todo="addTodo" @show-error-message="showErrorMessage" :todos="todos" />
    <main v-if="todos.length">
        <ul id="list-container">
            <li v-for="(todo, index) in todos" :key="index">
                <label :for="'todo-' + index">
                    <input type="checkbox" :id="'todo-' + index" v-model="todo.done" class="check-todo">
                    <del v-if="todo.done">{{ todo.task }}</del>
                    <span v-else>{{ todo.task }}</span>
                </label>
                <div>
                    <span class="todo-options" title="Excluir" @click="deleteTodo(index)">❌</span>
                    <span class="todo-options" title="Editar">✏️</span>
                </div>
            </li>
        </ul>
    </main>
    <div v-if="errorMsg !== ''" id="error-message">{{ errorMsg }}</div>
    <div v-if="deleting" id="delete-confirm-container">
        <div id="confirmation-box">
            <p>Essa task ainda não foi concluída, tem certeza que deseja excluí-la?</p>
            <div id="confirmation-buttons">
                <button class="confirm-btn" @click="confirmDeletion(true)">Sim</button>
                <button class="confirm-btn" @click="confirmDeletion(false)">Não</button>
            </div>
        </div>
    </div>
</template>

<script>
import FormTodo from './FormTodo.vue';

    export default{
        name: 'TodoList',
        components: {
            FormTodo
        },
        data(){
            return{
                todos: [],
                errorMsg: '',
                deleting: false,
                idToDelete: -1
            }
        },
        methods: {
            updateTodosOnLocalStorage(){
                localStorage.setItem('todos', JSON.stringify(this.todos));
            },

            addTodo(todo){
                this.todos.push(todo);
            },

            deleteTodo(id){
                if(!this.todos[id].done){
                    this.deleting = true;
                    this.idToDelete = id;
                } else{
                    this.removeTodo(id);
                }
            },

            confirmDeletion(isDeleting){
                if(isDeleting && this.idToDelete > -1)
                    this.removeTodo(this.idToDelete);
                this.deleting = false
                this.idToDelete = -1;
            },

            removeTodo(id){
                this.todos.splice(id, 1);
            },

            showErrorMessage(msg){
                this.errorMsg = msg;
                setTimeout(() => {
                    this.errorMsg = '';
                }, 5000);
            }
        },
        mounted(){
            this.todos = JSON.parse(localStorage.getItem('todos')) || [];
        },
        watch: {
            todos: {
                handler: 'updateTodosOnLocalStorage',
                deep: true
            }
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
        color: #686868;
    }

    #error-message{
        background-color: #E8363B;
        padding: 10px;
        border-radius: 5px;
        font-size: 14px;
        color: #fff;
        position: fixed;
        bottom: 7%;
        left: 50%;
        transform: translateX(-50%);
        z-index: 1;
    }

    #delete-confirm-container{
        background-color: #000000b6;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1;
        width: 100vw;
        height: 100vh;
    }

    #confirmation-box{
        background-color: #474747;
        position: fixed;
        top: 40%;
        left: 50%;
        transform: translate(-50%,-50%);
        padding: 15px;
        border-radius: 5px;
        width: 450px;
        color: var(--text-color);font-size: 18px;
    }

    #confirmation-buttons{
        display: flex;
        justify-content: center;
    }

    .confirm-btn{
        padding: 5px 9px;
        margin: 8px 4px 0 4px;
        font-size: 18px;
        background-color: #ffb951;
        color: #000;
        outline: none;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        &:hover{
            background-color: #ffa24c;
        }
    }
</style>