<script setup>
import { ref } from 'vue'
const lists = ref([])

fetch('http://localhost:3000/lists/', {
  method: 'GET',
  headers: { 'Content-Type': 'application/json' }
})
  .then((res) => res.json())
  .then((data) => (lists.value = data))
</script>

<template>
  <div v-for="list in lists" :key="list.id">
    <h2>{{ list.title }}</h2>
    <ul>
      <li v-for="item in list.items" :key="item.id">
        {{ item.itemName }}
        <input v-model="purchased" type="checkbox" />
        <addItem :itemProp="item" :list="list" />
      </li>
    </ul>
  </div>
</template>
=
