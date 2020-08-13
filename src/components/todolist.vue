<template>
  <b-container>
    <elem
      v-for="todo in todos"
      v-bind:todo="todo"
      :key="todo.id"
      v-on:remove-todo-item="removeTodoItem"
      v-on:toggle-todo-item="toggleTodoItem"
      v-on:edit-todo-item="editTodoItem"
    />
  </b-container>
</template>

<script>
import elem from "@/components/elem.vue";
export default {
  props: ["todos"],
  components: {
    elem
  },
  methods: {
    removeTodoItem(id) {
      this.$emit("remove-todo-item", id);
    },
    toggleTodoItem(id) {
      this.$emit("toggle-todo-item", id);
    },
    editTodoItem(id) {
      this.$emit("edit-todo-item", id);
    }
  }
};
</script>
