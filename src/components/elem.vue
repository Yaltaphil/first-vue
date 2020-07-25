<template>
  <transition name="fade">
    <b-row class="justify-content-md-center p-1">
      <b-col col="1" class="text-center">
        <b-form-checkbox
          v-model="todo.completed"
          v-on:click="todo.completed = !todo.completed"
        ></b-form-checkbox>
      </b-col>
      <b-col
        cols="8 pl-3"
        v-bind:class="{ done: todo.completed }"
        v-on:click="todo.completed = !todo.completed"
      >
        {{ todo.title }}
      </b-col>
      <b-col col="1" class="text-center">
        <b-button
          variant="outline-danger"
          v-on:click="$emit('removeTodoItem', todo.id)"
        >
          <p class="mb-0">
            <b-icon icon="trash"></b-icon>
          </p>
        </b-button>
      </b-col>
    </b-row>
  </transition>
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
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
