<template>
    <div id="form-todo">
        <h1 id="title">Todo App</h1>
        <div id="input-container">
            <input type="text" id="input-todo" v-model="task" @keyup.enter="addTodo">
            <button id="add-btn" @click="addTodo">
                <i class="fa fa-plus"></i>
            </button>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'FormTodo',
        props: {
            todos: Array
        },
        data(){
            return{
                task: ''
            }
        },
        methods: {
            addTodo(){
                this.task = this.task.trim();
                if(this.task.length >= 3){
                    const todoAlreadyExists = this.todos.some(todo => todo.task.toLowerCase() === this.task.toLowerCase());
                    if(!todoAlreadyExists){
                        this.$emit('add-todo', {
                            task: this.task,
                            done: false
                        });
                        this.task = '';
                    } else{
                        this.$emit('show-error-message', 'Ops, essa task já existe!');    
                    }
                } else if(this.task.length > 0){
                    this.$emit('show-error-message', 'A task deve ter no mínimo 3 caracteres para ser adicionada');
                }
            }
        }
    }
</script>

<style>
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

    @media screen and (max-width: 430px){
        #form-todo{
            margin: 26px 5px 5px 5px;
        }

        #input-container{
            width: 100%;
        }

        #input-todo{
            width: 90%;
        }

        #add-btn{
            width: 35px;
        }
    }

    @media screen and (max-width: 200px){
        #add-btn{
            padding: 5px 6px;
            width: 32px;
        }
    }
</style>