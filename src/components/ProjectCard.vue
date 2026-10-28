<script setup>
defineProps({
    project: Object
})
</script>

<template>
  <article>
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
