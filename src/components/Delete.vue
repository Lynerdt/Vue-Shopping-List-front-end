<script setup>
import { ref } from 'vue'
const deleteOk = ref(false)
const props = defineProps({ list: Object })
const emit = defineEmits(['listDeleted'])

const deleteList = (list) => {
  fetch('http://localhost:3000/lists/' + props.list.id, {
    method: 'DELETE'
  })
    .then((res) => res.json())
    .then((deletedList) => {
      emit('listDeleted', deletedList)
    })
}

function confirmDelete(e) {
  deleteOk.value = e
}
</script>

<template>
  <form>
    <button v-if="deleteOk" class="btn" @click="confirmDelete(false)">Don't Delete</button>
    <button v-else class="confirmDeleteBtn" @click="confirmDelete(true)">Delete List</button>
    <form class="deleteButton" v-if="deleteOk" @click.prevent="deleteList(list)">
      <button type="submit">Confirm Delete</button>
    </form>
  </form>
</template>
