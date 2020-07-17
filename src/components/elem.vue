<template>
  <tr>
    <td>{{ todo.id }}</td>
    <td>
      <input type="checkbox" />
    </td>
    <td>{{ todo.title }}</td>
    <td>
      <button>&times;</button>
    </td>
  </tr>
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
button {
  background-color: rgb(219, 84, 84);
}
</style>