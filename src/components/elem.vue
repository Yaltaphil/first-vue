<template>
  <tr>
    <td>{{ todo.id }}</td>
    <td>{{ todo.title }}</td>
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
