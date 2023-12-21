<script setup>
import { ref } from 'vue'
import ListofLists from './components/ListofLists.vue'
import createList from './components/createList.vue'
</script>

<template>
  <div>
    <h1>Buy Good Things</h1>
    <div class="make-list">
      <createList />
    </div>
    <ListofLists />
  </div>
</template>

<style scoped></style>
