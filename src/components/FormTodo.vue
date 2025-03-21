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
    export default{
        name: 'FormTodo'
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
</style>