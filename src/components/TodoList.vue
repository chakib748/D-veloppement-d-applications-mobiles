<template>
  <div>
    <h1>Liste of Todos</h1>
    <h3>{{ message }}</h3>
    <form name="todo-form" method="post" v-on:submit.prevent="addnewtodo">
      <label for="add-todo">add a new task</label><br />
      <input
        class="put"
        name="add-todo"
        placeholder="ex: sport à 16h00 "
        type="text"
        v-model="newTodo"
      />
      <button type="submit">add</button>
    </form>

    <div class="todo-lists" v-if="todos.length">
      <h3>My Todos</h3>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <input
            id="chps"
            :class="{ completed: todo.completed }"
            type="checkbox"
            v-on:blur="updateTask($event, todo)"
            v-on:change="completetask(todo)"
            v-bind:checked="todo.completed"
          />

          <span
            class="title"
            v-on:keydown.enter="updateTask($event, todo)"
            v-bind:class="{ completed: todo.completed }"
            >{{ todo.name }}
          </span>
          <button id="btn" v-on:click="removetodo(index)">Delet</button>
          <!--<button v-on:click="updateTask($event,todo)">Edit</button> !-->
        </li>
      </ul>
    </div>
    <div id="tache_re">
      <span >
        <strong>{{ nbr_tache_rest }}</strong> tache a faire</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "todolist",

  data() {
    return {
      todos: [],
      newTodo: "",
      filter: "all",
      nextTodo: "",
      message: "my todo list",
    };
  },
  methods: {
    removetodo(index) {
      if (confirm("Etes vous sur de supprimer cette tâche !! ")) {
        this.todos.splice(index, 1);
      }
    },
    addnewtodo() {
      if (this.newTodo != "") {
        this.todos.push({
          id: this.nextTodo,
          name: this.newTodo,
          completed: false,
        });
        (this.newTodo = ""), this.nextTodo++;
      }
    },
    /*
    updateTask(e, todo) {
      e.preventDefault();
      todo.name = e.target.innerText;
      e.target.blur();
    },
*/
    completetask(todo) {
      todo.completed = !todo.completed;
    },
  },
  computed: {
    nbr_tache_rest() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
li {
  list-style: none;
}
.completed {
  text-decoration: line-through;
}
/*
.todo-lists {
  background: burlywood;
  width: 50%;
  margin: auto;
}*/
form {
  background: white;
}
.put {
  background: #b0e0e6;
  width: 50%;
  padding: 12px 20px;
  margin: auto;
  box-sizing: border-box;
}
button {
  display: inline-block;
  background-color: blue;
  border-radius: 10px;
  border: 2px double #cccccc;
  color: #eeeeee;
  text-align: center;
  font-size: 15px;
  padding: 13px 13px;
  width: 100px;
  margin: 5px;
}
#btn {
  display: inline-block;
  background-color: rgb(255, 0, 0);
  border-radius: 10px;
  border: 2px double #cccccc;
  color: white;
  text-align: center;
  font-size: 15px;
  padding: 13px 13px;
  width: 100px;
  -webkit-transition: all 0.5s;
  -moz-transition: all 0.5s;
  -o-transition: all 0.5s;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}
#chps{
  background-color: red;
  width: 10%;
  padding: 12px 20px;
  margin: 10px;
  box-sizing: border-box;
}
#tache_re{
  background: #b0e0e6;
  width: 20%;
  padding: 12px 20px;
  margin:auto;
  box-sizing: border-box;
  border-radius: 20px;
}
</style>