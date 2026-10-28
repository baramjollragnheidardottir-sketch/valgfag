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
 <article v-for="project in projects">
  <h2>
   {{ project.title }}
  </h2>
  <p>
    {{ project.category }}
  </p> 
  <img :src="project.imageUrl" :alt="project.title"> 
  <p>
   {{ project.description }}
  </p>
 </article>

</template>

<style scoped>

</style>

