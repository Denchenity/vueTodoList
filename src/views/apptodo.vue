<template>
  <div>
    <h2>App TodoList</h2> 
    <router-link to="/">homepage</router-link>
    <hr>
    <AddTodo 
      v-bind:todos="todos"
      @new-todo="Addtodo"
    />
    <select v-model="filter">
      <option value="all">Все</option>
      <option value="completed">Отмеченные</option>
      <option value="no-completed">Не отмеченные</option>
    </select>
    <Loader v-if='loading'/>
    <Todolist 
      v-else-if='FilteredTodos.length'
      v-bind:todos="FilteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>Список пуст</p>
  </div>
</template>

<script>
import AddTodo from '@/components/addtodoitem';
import Todolist from '@/components/todolistnew';
import Loader from '@/components/Loader';



export default {
  name: 'App',
  data(){
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
  .then(response => response.json())
  .then(json => {
    setTimeout(() => {
      this.todos = json
      this.loading = false
    }, 1000);
  })
  },
  components: {
    Todolist,AddTodo,Loader
  },
  // watch:{
  //   filter(value){
  //     console.log(value)
  //   }
  // },
  computed:{
    FilteredTodos(){
      if(this.filter === 'all'){
        return this.todos
      }
      if(this.filter === 'completed'){
        return this.todos.filter(t => t.completed)
      }
      if(this.filter === 'completed'){
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  methods:{
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !== id)
    },
    Addtodo(todo){
      this.todos.push(todo)
    }
  }
}
</script>