<template>
  <b-container>
    <h2 class="text-center">Your TODO list</h2>
    <add @new-Item="addItem" />
    <hr />
    <todolist v-bind:todos="todos" v-on:rmTodo="rmTodo" v-if="todos.length" />
    <p v-else>No todos</p>
  </b-container>
</template>

<script>
import todolist from "@/components/todolist.vue";
import add from "@/components/add.vue";

export default {
  name: "App",
  components: {
    todolist,
    add
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=9")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
      });
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    addItem(Item) {
      console.log(Item);
      return this.todos.push(Item);
    },
    rmTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    }
  }
};
</script>
