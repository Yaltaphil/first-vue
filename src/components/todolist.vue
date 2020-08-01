<template>
  <b-container>
    <elem
      v-for="todo in todos"
      v-bind:todo="todo"
      :key="todo.id"
      v-on:removeTodoItem="removeTodoItem"
      v-on:toggleTodoItem="toggleTodoItem"
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
      this.$emit("removeTodoItem", id);
    },
    toggleTodoItem(id) {
      this.$emit("toggleTodoItem", id);
    }
  }
};
</script>
