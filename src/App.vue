<script setup>
import { ref } from  'vue'

const projects = ref([])
fetch("https://valgfag-9c07e-default-rtdb.europe-west1.firebasedatabase.app/.json")
  .then(response => response.json())
  .then(json => {
    projects.value = json
    console.log(projects.value)
    })
</script>

<template>
 
</template>

<style scoped>

</style>

