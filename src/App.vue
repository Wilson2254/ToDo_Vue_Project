<template>
  <div id="app">
        <link href="https://fonts.googleapis.com/css2?family=Odibee+Sans&display=swap" rel="stylesheet">
    <h1>Todo application</h1>
      <hr>
    <AddTodo
      @add-todo="addTodo"
    />
    <div class="main-sel">
      <div class="select">
        <select v-model="filter">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="not-completed">Not Completed</option>
        </select>
      </div>
    </div>

    <Loader v-if="loading"/>
    <TodoList
      v-else-if='filteredTodos.length'
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'app',
  data(){
    return {
      todos: [ ],
      loading: true,
      filter: 'all'
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
  .then(response => response.json())
  .then(json => {
    setTimeout(() =>{
      this.todos = json
      this.loading = false
    }, 1500)
  })
},
// warch: {
//   filter(value){
//
//   }
// },
computed:{
  filteredTodos(){
    if (this.filter === 'all'){
      return this.todos
    }

    else if (this.filter === 'completed'){
      return this.todos.filter(t => t.completed)
    }

    else{
      return this.todos.filter(t => !t.completed)
    }
  }
},
  methods:{
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo){
      this.todos.push(todo)
    }
  },
  components: {
    TodoList, AddTodo, Loader
  }
}
</script>

<style>
  #app{
    text-align: center;
    font-family: 'Odibee Sans';
    font-weight: bold;
    font-size: 20px;
  }
  .main-sel{
    display: flex;
    justify-content: center;
  }
  .select {
     position: relative;
     width: 20%;
     margin-top: 10px;
     display: flex;
     align-items: center;
 }
 .select select {
   display: block;
   width: 100%; /* от ширины блока div */
   padding: .75rem 2.5rem .75rem 1rem;/* отступы от текста до рамки */
   background: none; /* убираем фон */
   border: 1px solid #ccc; /* рамка */
   border-radius: 3px;/* скругление полей формы */
   -webkit-appearance: none;/* Chrome */
   -moz-appearance: none;/* Firefox */
   appearance: none;/* убираем дефолнтные стрелочки */
   font-family: inherit;/* наследует от родителя */
   font-size: 1rem;
   color: #444;
}
.select:after {
   content: "";
   display: flex;
   border-style: solid;
   border-width: 3px 3px 0 3px;
   border-color: #000 transparent transparent transparent;
   pointer-events: none;
   position: absolute;
   top: 50%;
   right: 1rem;
   z-index: 1;
   margin-top: -3px;
}

hr{
  width: 90%;
}
</style>
