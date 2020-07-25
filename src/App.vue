<template>
  <b-container fluid="sm">
    <h2 class="text-center my-3">Your TODO list</h2>
    <add @new-Item="addItem" />
    <b-row class="p-3">
      <b-form-group>
        <b-form-radio-group
          class="text-info"
          v-model="filter"
          :options="options"
        ></b-form-radio-group>
      </b-form-group>
    </b-row>
    <hr />
    <todolist
      v-bind:todos="displayTasks"
      v-on:removeTodoItem="removeTodoItem"
      v-if="todos.length"
    />
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
    if (localStorage.getItem("toDoList")) {
      this.todos = JSON.parse(localStorage.getItem("toDoList"));
    }
  },
  data() {
    return {
      todos: [],
      filter: "All",
      options: [
        { text: "All", value: "All" },
        { text: "Completed", value: "Completed" },
        { text: "Not completed", value: "Not completed" }
      ]
    };
  },
  computed: {
    displayTasks() {
      return this.todos.filter(t => {
        if (!this.filter || this.filter == "All") {
          return true;
        } else if (this.filter == "Completed") {
          return t.completed == true;
        } else if (this.filter == "Not completed") {
          return t.completed == false;
        }
      });
    }
  },
  methods: {
    addItem(Item) {
      this.todos.push(Item);
      localStorage.setItem("toDoList", JSON.stringify(this.todos));
    },
    removeTodoItem(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      localStorage.setItem("toDoList", JSON.stringify(this.todos));
    }
  }
};
</script>
