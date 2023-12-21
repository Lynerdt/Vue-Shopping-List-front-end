<script setup>
import { ref } from 'vue'
import addItem from './addItem.vue'
import createList from './createList.vue'
const addItem = ref('')
const props = defineProps({ itemProp: Object, list: Object })
const existingItems = ref(props.list[items])
const resetItem = () => {
  addItem.value = ''
}

const addNewItem = () => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: props.list.items.push({
        id: props.itemProp.id,
        itemName: addItem.value,
        purchased: 'false'
      }),
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((item) => {
      resetItem()
    })
}
</script>

<template>
  <form class="itemForm" @submit.prevent="addNewItem">
    <input v-model="addItem" type="text" placeholder="New Item" />
    <button type="submit">Add</button>
  </form>
</template>
