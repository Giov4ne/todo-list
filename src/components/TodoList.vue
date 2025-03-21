<template>
    <FormTodo @add-todo="addTodo" @show-error-message="showErrorMessage" :todos="todos" />
    <main v-if="todos.length">
        <ul id="list-container">
            <li v-for="(todo, index) in todos" :key="index">
                <label :for="'todo-' + index">
                    <input type="checkbox" :id="'todo-' + index" v-model="todo.done" class="check-todo">
                    <input v-if="indexToEdit === index" :value="todo.task" @keyup.enter="editTodo($event.target.value)" @blur="editTodo($event.target.value)" type="text" id="edit-input" selected>
                    <del v-else-if="todo.done">{{ todo.task }}</del>
                    <span v-else>{{ todo.task }}</span>
                </label>
                <div>
                    <span class="todo-options" title="Excluir" @click="deleteTodo(index)">❌</span>
                    <span class="todo-options" title="Editar" @click="selectTodoToEdit(index)">✏️</span>
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
                indexToDelete: -1,
                indexToEdit: -1
            }
        },
        methods: {
            updateTodosOnLocalStorage(){
                localStorage.setItem('todos', JSON.stringify(this.todos));
            },

            addTodo(todo){
                this.todos.push(todo);
            },

            deleteTodo(index){
                if(!this.todos[index].done){
                    this.deleting = true;
                    this.indexToDelete = index;
                } else{
                    this.removeTodo(index);
                }
            },

            confirmDeletion(isDeleting){
                if(isDeleting && this.indexToDelete > -1)
                    this.removeTodo(this.indexToDelete);
                this.deleting = false
                this.indexToDelete = -1;
            },

            removeTodo(index){
                this.todos.splice(index, 1);
            },

            selectTodoToEdit(index){
                this.indexToEdit = index;
                this.$nextTick(() => {
                    const editInput = document.getElementById('edit-input');
                    editInput.focus();
                    editInput.select();
                });
            },

            editTodo(newTask){
                if(this.indexToEdit > -1){
                    newTask = newTask.trim();
                    const todoAlreadyExists = this.todos.some((todo, index) => index !== this.indexToEdit && todo.task.toLowerCase() === newTask.toLowerCase());
                    if(todoAlreadyExists)
                        this.showErrorMessage('Ops, essa task já existe!');
                    else if(newTask.length < 3)
                        this.showErrorMessage('A task deve ter no mínimo 3 caracteres');
                    else
                        this.todos[this.indexToEdit].task = newTask;
                }
                this.indexToEdit = -1;
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
        border-bottom: 1px solid var(--color1);
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
            accent-color: var(--color1);
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
        color: var(--color2);
    }

    #error-message{
        background-color: var(--error-message-color);
        padding: 10px;
        border-radius: 5px;
        font-size: 14px;
        color: var(--text-color);
        position: fixed;
        bottom: 7%;
        left: 50%;
        transform: translateX(-50%);
        z-index: 1;
    }

    #delete-confirm-container{
        background-color: var(--third-background-color);
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1;
        width: 100vw;
        height: 100vh;
    }

    #confirmation-box{
        background-color: var(--second-background-color);
        position: fixed;
        top: 40%;
        left: 50%;
        transform: translate(-50%,-50%);
        padding: 15px;
        border-radius: 5px;
        width: 450px;
        color: var(--text-color);
        font-size: 18px;
    }

    #confirmation-buttons{
        display: flex;
        justify-content: center;
    }

    .confirm-btn{
        padding: 5px 9px;
        margin: 8px 4px 0 4px;
        font-size: 18px;
        background-color: var(--color1);
        color: var(--color4);
        outline: none;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        &:hover{
            background-color: var(--main-hover-color);
        }
    }

    #edit-input{
        font-size: 18px;
        outline: none;
        border: none;
        background-color: transparent;
        color: var(--text-color);
    }

    @media screen and (max-width: 670px){
        #list-container li{
            width: 90vw;
        }
    }

    @media screen and (max-width: 490px){
        #confirmation-box{
            width: 90%;
        }
    }

    @media screen and (max-width: 230px){
        #list-container li label{
            word-break: break-all;
            margin-right: 4px;
        }

        #list-container li label .check-todo{
            margin-right: 4px;
            min-width: 15px;
            min-height: 15px;
        }

        #list-container li .todo-options{
            margin-left: 1px;
            font-size: 18px;
        }
    }
</style>