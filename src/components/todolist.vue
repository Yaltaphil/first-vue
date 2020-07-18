<template>
  <b-container>
    <elem
      v-for="todo in todos"
      v-bind:todo="todo"
      :key="todo.id"
      v-on:rmTodo="rmTodo"
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
    rmTodo(id) {
      this.$emit("rmTodo", id);
    }
  }
};
</script>
