<template>
    <div>
        <form @submit="onSubmit">
            <input type="text" v-model="title" placeholder="Please Enter The Title">
            <input type="submit" value="submit">
        </form>
        <h1>Hello Vuex</h1>
        <FilteredTodos/>
        <div class="todos">
           <Todo v-for="todo in allTodos" :key="todo.id" :todo="todo"/>
            <!-- <p>Unque ID: {{todo.id}} </p>
            <p>Title: {{todo.title}}</p>
            <p>status: {{todo.completed}}</p> -->
        </div>
    </div>
</template>
<script>
import {mapGetters, mapActions} from 'vuex';
import Todo from './Todo'
import FilteredTodos from './FilteredTodos';
export default {
    name: 'Todos',
    data(){
        return{
            title: ''
        }
    },
    components: {
        Todo,
        FilteredTodos
    },
    methods:{
        ...mapActions(['fetchTodos','addTodo']),
        onSubmit(e){
            e.preventDefault();
            this.addTodo(this.title);
            // console.log(this.title)
            this.title = ''
        },
        
    },
    computed: mapGetters(['allTodos']),
    created(){
        this.fetchTodos();
    }
    
    
}
</script>
<style scoped>
.todos{
    background-color: #A17EE0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}
</style>