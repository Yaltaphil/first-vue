<template>
  <form @submit.prevent="onSubmit">
    <b-input-group size="lg" prepend="New task">
      <b-form-input v-model="title" placeholder="type here"></b-form-input>
      <b-button
        type="submit"
        variant="outline-success"
        v-b-tooltip.hover
        title="Add me! Add me!"
        ><b-icon icon="box-arrow-in-down"></b-icon> Add
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
      }
    }
  }
};
</script>
