<template>
  <div>
    <table>
      <elem v-for="todo in todos" v-bind:todo="todo" :key="todo.title" />
    </table>
  </div>
</template>


<script>
import elem from "@/components/elem.vue";
export default {
  props: ["todos"],
  components: {
    elem
  }
};
</script>
 