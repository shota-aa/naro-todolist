<template>
  <div>TodoList</div>
  <div>完了したタスク</div>
  <div v-for="item in items" :key="item.todo">
    <div v-if="item.status == true">
      <a>{{ item.name }} &nbsp;</a>
      <button @click="changeToUncompleted(item)">↓</button>
      <br />
    </div>
  </div>
  <br />
  <div>未完了のタスク</div>
  <div v-for="item in items" :key="item.todo">
    <div v-if="item.status == false">
      <a>{{ item.name }} &nbsp;</a>
      <button @click="changeToCompleted(item)">↑</button>
      <br />
    </div>
  </div>
  <label>
    追加するタスクの名前
    <input v-model="newItemName" type="text" />
    <button @click="addItem">add</button>
  </label>
</template>

<script>
import { ref } from "vue";

export default {
  name: "TodoList",
  setup() {
    const items = ref([
      { name: "お菓子買う", status: true },
      { name: "寝る", status: false },
    ]);
    const newItemName = ref("");

    const addItem = () => {
      items.value.push({ name: newItemName.value, status: false });
      newItemName.value = "";
    };

    const changeToUncompleted = (item) => {
      item.status = false;
    };
    const changeToCompleted = (item) => {
      item.status = true;
    };

    return {
      items,
      newItemName,
      addItem,
      changeToCompleted,
      changeToUncompleted,
    };
  },
};
</script>
