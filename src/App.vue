<template>
  <div class="app">
    <md-field>
      <md-input
        class="input" 
        v-model="currentTodo" 
        @keydown.enter="addTodo()" 
        placeholder="Add a todo"></md-input>
    </md-field>
    
    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <span 
          class="list-item"
          v-if="!todo.editTodo"
          :class="{completed: todo.completed}" 
          @dblclick="editedTodo(todo)">
          {{todo.title}}
        </span>
        <input 
          v-if="todo.editTodo" 
          v-model="todo.title" 
          @keydown.enter="doneEdit(todo)" 
        />
        <input class="checkbox" @click="completedTodo(todo)" type="checkbox" >
        <p class="delete" @click="removeTodo(todo)">X</p>
      </li>
    </ul>
  </div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
}

body{
  background-color: #07173D;
}

.title{
  text-align: center;
  color: #41B883;
  margin: 25px 0;
  font-size: 42px;
}

.app{
  max-width: 700px;
  margin: 30px auto;
  background-color: #fff;
}

.todos li{
  border-top: 1px solid #000;
  list-style: none;
  background-color: #758DA9;
  padding: 10px;
  font-size: 25px;

}

.delete{
  float: right;
  font-weight: 700;
  background-color: Transparent;
  margin: 0 10px 0 0;
  border: none;
  cursor:pointer;
  color: red;
  font-size: 24px;
}

.checkbox{
  float: right;
  width: 20px;
  height: 20px;
}

.completed{
  text-decoration: line-through;
}

</style>

<script>

export default {
  data(){
    return {
      todos: [],
      currentTodo: ""
    };
  },
  methods: {
    addTodo(){
      if(this.currentTodo){
        this.todos.push({
          id: this.todos.length,
          title: this.currentTodo,
          completed: false,
          editTodo: null
        });
        this.currentTodo = "";
      }
    },
    removeTodo(todo){
      let index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editedTodo(todo){
      todo.editTodo = todo;
    },
    doneEdit(todo){
      todo.title = todo.title.trim();
      todo.editTodo = null;
    },
    completedTodo(todo){
      if(!todo.completed){
        todo.completed = true;
      }else{
        todo.completed = false;
      }
    }
  }
}
</script>

