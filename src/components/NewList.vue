<script setup>
import { ref } from 'vue'
const newList = ref('')
const addingList = ref(false)
const emit = defineEmits(['listAdded'])

const createList = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ title: newList.value, items: [], updatedAt: new Date() })
  })
    .then((res) => res.json())
    .then((newList) => {
      emit('listAdded', newList)
      resetList()
    })
}
const addList = (e) => {
  addingList.value = e
}
const resetList = () => {
  newList.value = ''
}
</script>

<template>
  <button v-if="addingList" @click="addList(false)">Cancel</button>
  <button v-else @click="addList(true)">Create List</button>
  <form v-if="addingList" class="newList" @submit.prevent="createList">
    <input v-model="newList" type="text" placeholder="Where to Shop?" />
    <button type="submit">Create</button>
  </form>
</template>
