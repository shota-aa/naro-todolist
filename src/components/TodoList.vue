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
  <div v-for="item in sortedItems" :key="item.todo">
    <div v-if="item.status == false">
      <a>{{ item.priority }}: {{ item.name }} &nbsp;</a>
      <button @click="changeToCompleted(item)">↑</button>
      <button @click="changePriority(item)">priority</button>
      <br />
    </div>
  </div>
  <label>
    追加するタスクの名前
    <input v-model="newItemName" type="text" />
    <button @click="addItem">add</button>
    優先順位入力
    <input v-model.number="inputPriority" type="number" />
  </label>
</template>

<script>
import { ref } from "vue";

export default {
  name: "TodoList",
  setup() {
    const items = ref([
      { name: "お菓子買う", status: true, priority: 0 },
      { name: "寝る", status: false, priority: 1 },
    ]);
    const newItemName = ref("");
    const inputPriority = ref(0);

    const addItem = () => {
      items.value.push({
        name: newItemName.value,
        status: false,
        priority:
          Math.max.apply(
            null,
            items.value.map(function (i) {
              return i.priority;
            })
          ) + 1,
      });

      newItemName.value = "";
    };

    var sortedItems = items.value.sort(function (a, b) {
      return a.priority - b.priority;
    });
    const changeToUncompleted = (item) => {
      item.status = false;
      item.priority =
        Math.max.apply(
          null,
          items.value.map(function (i) {
            return i.priority;
          })
        ) + 1;
      sortedItems = items.value.sort(function (a, b) {
        return a.priority - b.priority;
      });
    };
    const changeToCompleted = (item) => {
      item.status = true;
      item.priority = 0;
      sortedItems = items.value.sort(function (a, b) {
        return a.priority - b.priority;
      });
    };
    const changePriority = (item) => {
      item.priority = inputPriority.value;
      inputPriority.value = 0;
      sortedItems = items.value.sort(function (a, b) {
        return a.priority - b.priority;
      });
    };

    return {
      items,
      newItemName,
      addItem,
      changeToCompleted,
      changeToUncompleted,
      changePriority,
      inputPriority,
      sortedItems,
    };
  },
};
</script>
