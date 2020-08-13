<template>
  <transition name="fade">
    <b-row class="justify-content-md-center p-1">
      <b-col cols="1" class="text-center">
        <b-form-checkbox
          v-model="todo.completed"
          v-on:change="$emit('toggle-todo-item', todo.id)"
        ></b-form-checkbox>
      </b-col>
      <b-col
        cols="9"
        class="pl-3"
        v-bind:class="{ done: todo.completed }"
        v-on:click="$emit('toggle-todo-item', todo.id)"
        >{{ todo.title }}</b-col
      >

      <b-col cols="1" class="text-center">
        <b-button
          variant="outline-info"
          v-on:click="$emit('edit-todo-item', todo.id)"
        >
          <b-icon icon="pencil"></b-icon>
        </b-button>
      </b-col>
      <b-col cols="1" class="text-center">
        <b-button
          variant="outline-danger"
          v-on:click="$emit('remove-todo-item', todo.id)"
        >
          <b-icon icon="trash"></b-icon>
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
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
