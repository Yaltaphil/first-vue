<template>
  <b-row class="justify-content-md-center">
    <b-col col="1" class="text-center">
      <b-form-checkbox
        v-model="todo.completed"
        v-on:click="todo.completed = !todo.completed"
      ></b-form-checkbox>
    </b-col>
    <b-col cols="10" v-bind:class="{ done: todo.completed }">
      {{ todo.title }}
    </b-col>
    <b-col col="1" class="text-center">
      <b-button variant="outline-danger" v-on:click="$emit('rmTodo', todo.id)">
        <b-icon icon="trash"></b-icon>
      </b-button>
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
