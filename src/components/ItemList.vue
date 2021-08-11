<template>
  <div>ItemList</div>
  <div v-for="item in items" :key="item.name">
    <div class="item" :class="{ over500: item.price >= 500 }">
      <div class="name">名前: {{ item.name }}</div>
      <div class="price">{{ item.price }} 円</div>
      <div v-if="item.price >= 10000">高額商品</div>
    </div>
  </div>
  <div>
    <label>
      名前
      <input v-model="newItemName" type="text" />
    </label>
    <label>
      価格
      <input v-model="newItemPrice" type="text" />
      <button @click="addItem">add</button>
    </label>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "ItemList",
  setup() {
    const items = ref([
      { name: "たまご", price: 100 },
      { name: "りんご", price: 160 },
      { name: "多岐", price: 10009 },
    ]);
    const newItemName = ref("");
    const newItemPrice = ref(0);

    const addItem = () => {
      if (newItemName.value == "" && newItemPrice.value == 0) {
        return;
      }
      items.value.push({ name: newItemName.value, price: newItemPrice.value });
      newItemName.value = "";
      newItemPrice.value = 0;
    };

    return { items, newItemName, newItemPrice, addItem };
  },
};
</script>

<style>
.over500 {
  color: red;
}
</style>
