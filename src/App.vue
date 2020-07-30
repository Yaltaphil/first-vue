<template>
  <b-container fluid="sm">
    <h3 class="text-center my-2">Your TODO list</h3>
    <add @new-Item="addItem" />
    <b-row class="p-2 ml-3">
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
      v-if="displayTasks.length"
    />
    <b-alert v-else show fade variant="info">No items in this category</b-alert>

    <footer class="navbar footer fixed-bottom">
      <b-alert show fade dismissible class="mx-auto">
        All tasks stored in your browser's local storage ...
        <b-button
          href="https://money.yandex.ru/to/410013014746086"
          variant="outline-info"
          target="_blank"
        >
          <b-icon icon="hand-thumbs-up"></b-icon> Donate
        </b-button>
      </b-alert>
    </footer>
  </b-container>
</template>

<script>
import todolist from "@/components/todolist.vue";
import add from "@/components/add.vue";
var addSound = new Audio(require("@/assets/End_note.ogg"));
addSound.volume = 0.35;
var trashSound = new Audio(require("@/assets/KeypressStandard.ogg"));
trashSound.volume = 0.5;
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
      addSound.play();
    },
    removeTodoItem(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      localStorage.setItem("toDoList", JSON.stringify(this.todos));
      trashSound.play();
    }
  }
};
</script>
<style>
body {
  background: linear-gradient(to right, #ddf6ff, #80cef8);
}
</style>
