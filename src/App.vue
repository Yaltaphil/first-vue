<template>
  <div id="app">
    <h1>Your TODO list</h1>
    <add @new-Item="addItem"/>
    <todolist v-bind:todos='todos'/>
  </div>
</template>

<script>
import todolist from "@/components/todolist.vue";
import add from "@/components/add.vue";

export default {
  name: "App",
  components: {
    todolist,
    add
  },
  data() {
    return {
      todos: [{id:1, title: "Read books every day", checked: false }, 
      {id:2, title: "Sleep enough", checked: false },
      {id:3, title: "Be calm and make sport sessions", checked: false }],
        };
    
  },
  methods: {
    addItem(Item) {
      console.log(Item)
      return this.todos.push(Item);
    }    
  }
};
</script>
