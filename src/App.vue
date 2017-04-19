<template>
  <div id="app">
      <todos></todos>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
    name: 'app',
    data(){
        return {
            todos:[
                {id:null, title:'It is cool', completed:true},
                {id:null, title:'It is cool', completed:false},
                {id:null, title:'It is cool', completed:true}
            ]
        }
    },
    computed:{
        todoCount() {
            return this.todos.length;
        }
    },
    components:{
        Todos
    }
}
</script>


