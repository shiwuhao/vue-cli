<template>
  <div id="todos">
    <ul class="list-group">
      <li class="list-group-item" v-for="(todo, index) in todos" v-bind:class="{'computed':todo.computed}">
        <router-link :to="{ name: 'todo', params: { id: todo.id }}">{{ todo.body }}</router-link>
        <div class="pull-right">
          <button class="btn btn-xs" @click="completeTodo(todo)" v-bind:class="[todo.computed ? 'btn-warning' : 'btn-success']">
            {{ todo.computed ? 'cancel' : 'computed' }}
          </button>
          <button class="btn btn-danger btn-xs" @click="deleteTodo(index)">remove</button>
        </div>
      </li>
    </ul>
      <todo-form :todos="todos"></todo-form>
  </div>
</template>

<script>
import TodoForm from './TodoForm'
export default {
    name: 'todos',
    data(){
        return {
            todos:[]
        }
    },
    methods:{
        deleteTodo(index) {
            this.todos.splice(index, 1);
        },
        completeTodo(todo) {
            todo.computed = !todo.computed;
        }
    },
    components:{
        TodoForm
    },
    mounted(){
        this.axios.get('http://laravel-vue.dev/api/todos').then(response => {
            this.todos = response.data;
        });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .computed{ color: green; text-decoration: line-through; }
</style>
