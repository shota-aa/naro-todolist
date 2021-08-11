<template>
  <div>
    <h1>{{ msg }}</h1>
    <counter />
    <item-list />
    <todo-list />
  </div>
</template>

<script>
import Counter from "./Counter.vue";
import ItemList from "./ItemList.vue";
import TodoList from "./TodoList.vue";

export default {
  components: {
    Counter,
    ItemList,
    TodoList,
  },
  props: {
    msg: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
