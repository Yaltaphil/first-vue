<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" placeholder="type here" />
    <button type="submit">ADD</button>
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
          title: this.title
        };
        this.$emit("new-Item", newTodo);
        this.title ='';    
      }
    }
  }
};
</script>