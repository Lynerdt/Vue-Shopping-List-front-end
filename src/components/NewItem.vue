<script setup>
import { ref } from 'vue'

const newItem = ref('')
const addingItem = ref(false)

const props = defineProps({ list: Object })
const emit = defineEmits(['itemAdded'])

const addNewItem = () => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [
        ...props.list.title,
        {
          id: props.list.items.length + 1,
          itemName: newItem.value,
          purchased: false
        }
      ],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((addeditem) => {
      emit('itemAdded', addeditem)
      resetItem()
    })
}
const addItem = (e) => {
  addingItem.value = e
}

const resetItem = () => {
  newItem.value = ''
}
</script>

<template>
  <div>
    <form v-if="addingItem" class="itemForm" @submit.prevent="addNewItem">
      <input v-model="newItem" type="text" placeholder="Add Item" />
      <button type="submit">Add</button>
    </form>
    <button v-if="addingItem" @click="addItem(false)">Don't Add</button>
    <button v-else @click="addItem(true)">Add Item</button>
  </div>
</template>
