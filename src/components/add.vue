<template>
  <form @submit.prevent="onSubmit">
    <b-input-group prepend="New task">
      <b-form-input
        v-model="title"
        placeholder="type here"
        aria-controls="field for task input"
        ref="todoInput"
      ></b-form-input>
      <b-button type="submit" variant="success">
        <b-icon icon="box-arrow-in-down"></b-icon> Add
      </b-button>
    </b-input-group>
  </form>
</template>

<script>
export default {
  data() {
    return { title: "" };
  },
  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        };
        this.$emit("new-Item", newTodo);
        this.title = "";
        this.$refs.todoInput.focus();
      }
    }
  }
};
</script>
