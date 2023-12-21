<script setup>
import { ref } from 'vue'
const createList = ref('')
const resetList = () => {
  createList.value = ''
}
const addList = () => {
  fetch('http://localhost:3000/lists/', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ title: createList.value, items: [], updatedAt: new Date() })
  })
    .then((res) => res.json())
    .then((list) => {
      resetList()
    })
}
</script>

<template>
  <form class="createList" @submit.prevent="addList">
    <input v-model="createList" type="text" placeholder="Where to Shop?" />

    <input class="button" type="submit" value="Create List" />
  </form>
</template>
