<script setup>
import { ref } from 'vue'
import Delete from './Delete.vue'

const props = defineProps({ list: Object })
const editing = ref(false)
const togglePurchased = (items) => {
  items.purchased = !items.purchased
  purchasedItem(props.list)
}
const makeEdit = (e) => {
  editing.value = e
}
const purchasedItem = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'PATCH',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      title: props.list.title,
      items: [...props.list.items],
      updatedAt: new Date()
    })
  })
    .then((res) => res.json())
    .then((r) => {})
}
</script>

<template>
  <div>
    <h3>{{ props.list.title }}: {{ props.list.items.length }} Items</h3>
    <div>
      <button v-if="editing" @click="makeEdit(false)">Don't Show List</button>
      <button v-else @click="makeEdit(true)">Show List</button>
      <div v-if="editing">
        <ul>
          <li
            v-for="items in props.list.items"
            @click="togglePurchased(items)"
            :key="list.items.id"
            :class="{ strikeout: items.purchased }"
          >
            {{ items.itemName }}
            <input v-model="items.purchased" type="checkbox" />
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
