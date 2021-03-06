<template>
  <b-container fluid="sm">
    <b-navbar toggleable="true" type="light" variant="outline-info">
      <b-navbar-brand>
        <h3>Your TODO list</h3>
      </b-navbar-brand>
      <b-navbar-toggle
        v-b-tooltip.hover
        title="Settings"
        target="nav-collapse"
      ></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="border">
          <label>
            <b-form-checkbox
              v-model="settings.soundOn"
              switch
              class="py-3 mx-3"
            >
              Sounds:
              <b>{{ settings.soundOn ? "on" : "off" }}</b>
            </b-form-checkbox>
          </label>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <add v-on:new-item="addItem" />

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
      v-on:edit-todo-item="editTodoItem"
      v-on:remove-todo-item="removeTodoItem"
      v-on:toggle-todo-item="toggleTodoItem"
      v-if="displayTasks.length"
    />
    <b-alert v-else fade show variant="light">No items in category</b-alert>

    <b-modal
      id="edit-modal"
      title="Edit task"
      ok-only
      header-bg-variant="success"
    >
      <b-form-input
        v-model.lazy="taskToEdit.title"
        v-on:keydown.enter="closeModal"
        autofocus
      ></b-form-input>
    </b-modal>

    <footer class="navbar footer fixed-bottom">
      <b-alert class="mx-auto" fade show="20">
        All tasks stored in your browser's local storage ...
        <b-button
          href="https://money.yandex.ru/to/410013014746086"
          variant="outline-info"
          target="_blank"
        >
          <b-icon icon="hand-thumbs-up"></b-icon>Donate
        </b-button>
      </b-alert>
    </footer>
  </b-container>
</template>

<script>
import todolist from "@/components/todolist.vue";
import add from "@/components/add.vue";

const addSound = new Audio(require("@/assets/End_note.ogg"));
addSound.volume = 0.35;
const trashSound = new Audio(require("@/assets/NFCTransferComplete.ogg"));
trashSound.volume = 0.5;
const toggleSound = new Audio(require("@/assets/KeypressStandard.ogg"));
toggleSound.volume = 0.7;

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
    if (localStorage.getItem("todoSettings")) {
      this.settings = JSON.parse(localStorage.getItem("todoSettings"));
    }
  },
  updated() {
    localStorage.setItem("toDoList", JSON.stringify(this.todos));
    localStorage.setItem("todoSettings", JSON.stringify(this.settings));
  },

  data() {
    return {
      todos: [],
      filter: "All",
      settings: {
        soundOn: true
      },
      taskToEdit: "",
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
        if (this.filter === "All") {
          return true;
        } else if (this.filter === "Completed") {
          return t.completed === true;
        } else if (this.filter === "Not completed") {
          return t.completed === false;
        }
      });
    }
  },
  methods: {
    addItem(newItem) {
      this.todos.push(newItem);
      this.settings.soundOn && addSound.play();
    },
    removeTodoItem(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      this.settings.soundOn && trashSound.play();
    },
    toggleTodoItem(id) {
      let toggleElem = this.todos.find(t => t.id === id);
      toggleElem.completed = !toggleElem.completed;
      this.settings.soundOn && toggleSound.play();
    },
    editTodoItem(id) {
      this.taskToEdit = this.todos.find(t => t.id === id);
      this.$bvModal.show("edit-modal");
    },
    closeModal() {
      this.settings.soundOn && addSound.play();
      this.$bvModal.hide("edit-modal");
    }
  }
};
</script>
<style>
body {
  background: linear-gradient(to right, #ddf6ff, #80cef8);
}
</style>
