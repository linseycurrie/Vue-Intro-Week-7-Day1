<template>
  <div id="app">


    <ul>
      <li v-for="(todo, index) in todos"
          v-bind:class="todo.complete ? 'complete' : 'not-complete'"
          :key="index">
          <span>{{ todo.activity }}</span>
          <span v-if="todo.complete">Complete!</span>
        
          <span v-if="todo.priority == 'high'">High</span>
          <span v-else-if="todo.priority == 'low'">Low</span>
          <span v-else></span>
          <button v-if="!todo.complete" v-on:click="completeTodo(index)">Mark as Complete</button>
      </li>
    </ul>
    
    <form v-on:submit.prevent="addNewTodo">
      <label for="new-todo">Add New Todo</label>
      <input type="text" id="new-todo" v-model="newTodo"/>

          <p>Priority</p>
      <div>
        <label for="high">High</label>
        <input type="radio" value="high" id="high" v-model="priority">
      </div>
      <div>
        <label for="low">Low</label>
        <input type="radio" value="low" id="low" v-model="priority">
      </div>

      <input type="submit" value="Save New Todo" />
    </form>

  </div>
</template>

<script>
export default {
  data(){
    return {
      todos: [
        {activity: "Clean Bathroom", complete: false, priority: "high"},
        {activity: "Food Shopping", complete: false, priority: "high"},
        {activity: "Car's MOT", complete: false, priority: "high"},
        {activity: "Cut Grass", complete: false, priority: "high"},
      ],
      newTodo: "",
    }
  },
  methods: {
    addNewTodo: function(){
      this.todos.push({
        activity: this.newTodo,
        complete: false,
        priority: this.priority,
      });
      this.newTodo = "";
    },

    completeTodo: function(index){
      this.todos[index].complete = true;
      this.priority = "";
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  width: 60%;
}

ul {
  list-style-type: none;
}

li span {
  padding: 20px;
}

li button{
  padding: 10px;
  cursor: grab;
}

button, input[type="submit"]{
  cursor: grab;
}

li.complete {
  border: 5px solid rgb(153, 253, 4);
  padding: 10px;
}

li.not-complete {
  border: 5px solid red;
  padding: 10px;
}

input[type="text"] {
  padding: 10px;
  width: 60%;
  margin: 5px;
}
</style>
