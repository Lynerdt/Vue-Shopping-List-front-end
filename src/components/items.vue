<script setup>
import { ref } from 'vue'

const props = defineProps({ item: String })
</script>

<template>
  <div>
    {{ props.item }}
  </div>
</template>
