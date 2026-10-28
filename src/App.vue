<script setup>
import { ref } from  'vue'
import ProjectCard from './components/ProjectCard.vue'

const projects = ref([])
fetch("https://valgfag-9c07e-default-rtdb.europe-west1.firebasedatabase.app/.json")
  .then(response => response.json())
  .then(json => {
    projects.value = json
    console.log(projects.value)
    })
</script>

<template>
 <projectCard
 v-for="(project, index) in projects"
 :key="index"
 :project="project"
 />

</template>

<style scoped>

</style>

