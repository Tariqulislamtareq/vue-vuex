<template>
    <div @dblclick="onDoubleClick(todo)" class="todo" :class="cmptClass" >
        <p>Unque ID: {{uId}} </p>
        <p>Title: {{title}}</p>
        <p>status: {{isCompleted}}</p>
        <p class="delete" @click="deleteTodo(uId)">Delete</p>
    </div>
</template>
<script>
import {mapActions} from 'vuex';
export default {
    name: 'Todo',
    props:{
        todo:{
            type: Object,
            required: true,
        }
    },
    computed:{
        uId(){
            return this.todo.id
        },
        title(){
            return this.todo.title
        },
        isCompleted(){
            if (this.todo.completed){
                return 'Completed'
            }else{
                return 'Not Completed'
            }
        },
        cmptClass(){
            if(this.todo.completed){
                return 'completed'
            }else{
                return 'notCompleted'
            }
        }
    },
    methods:{
        ...mapActions(['deleteTodo', 'updateTodo']),
        onDoubleClick(todo){
            const updatedTodo = {
                id: todo.id,
                title: todo.title,
                completed: !todo.completed
            }
            this.updateTodo(updatedTodo)
        }
    }
}
</script>
<style scoped>
.todo{
    width: 200px;
    height: auto;
    border: 1px solid #ffffff;
    color: #ffffff;
    margin: 2px;
    padding: 2px;
}
.completed{
    background-color: #159957;
}
.notCompleted{
    background-color: #CB2D3E;
}
.delete{
    color: #ffffff;
    cursor: pointer;
}
</style>