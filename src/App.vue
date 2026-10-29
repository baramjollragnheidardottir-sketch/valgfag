<script setup>
import { ref } from  'vue'
import ProjectCard from './components/ProjectCard.vue'
import ProjectForm from './components/ProjectForm.vue'

const projects = ref([])
const currentIndex = ref(0)
const myProject = ref(null)

function nextProject() {
  currentIndex.value = (currentIndex.value + 1) % projects.value.length
}
function previousProject() {
  currentIndex.value = (currentIndex.value - 1 + projects.value.length) % projects.value.length
}

fetch("https://valgfag-9c07e-default-rtdb.europe-west1.firebasedatabase.app/.json")
  .then(response => response.json())
  .then(json => {
  projects.value = Array.from({ length: 6 }, (_, index) => json[index])
  myProject.value = json.myProject ?? null

  console.log(projects.value)
  console.log(myProject.value)
})

</script>

<template>
  <h1 class="hero-title">My Projects</h1>

  <div class="project-gallery">
 
    <ProjectCard
     v-if="projects.length"
   :project="projects[currentIndex]">
  
    <template #carousel>
      <div class="carousel">

       <button 
         class="carousel-button" 
         type="button" 
         @click="previousProject" 
         aria-label="Previous project">
          ← 
       </button>
      
      <div class="carousel-dots">
      
        <button 
         v-for="(project, index) in projects"
         :key="index"
         class="carousel-dot"
         :class="{ active: currentIndex === index }"
         type="button"
         @click="currentIndex = index"
         :aria-label="`Go to project ${index + 1}`"
         :aria-current="currentIndex === index ? 'true' : undefined"
        >
        </button>
      </div>

      <button 
       class="carousel-button" 
       type="button" 
       @click="nextProject"
       aria-label="Next project"
      >
        →
      </button>

      </div>
     
   </template>
   </ProjectCard>
  </div>

  <h2 class="hero-title">Add your own project</h2>

  <ProjectForm 
   :projects="projects" 
   @projectSaved="myProject = $event"
  />

  <ProjectCard
  v-if="myProject"
  :project="myProject"
  />
</template>

<style scoped>
.hero-title {
  font-size: var(--font-size-hero);
  font-family: var(--font-primary);
  color: var(--color-title);
  width: fit-content;
  border-bottom: 0.2rem solid currentColor;
  margin-top: 2rem;
  margin-bottom: 4rem;
}

 .project-gallery {
   display: grid;
   align-items: center;
   gap: 1rem;
   grid-template-columns: 1fr;
 }

 .carousel {
   display: flex;
   justify-content: space-between;
   align-items: center;
   padding-block: 1.5rem;
 }

 .carousel-button {
   background: transparent;
   border: none;
   color: var(--color-text);
   font-size: 5rem;
   line-height: 1;
   padding: 0;
   cursor: pointer;
 }

 .carousel-dots {
   display: flex;
   align-items: center;
   gap: 1.5rem;
 }

 .carousel-dot {
   width: 1.5rem;
   height: 1.5rem;
   padding: 0;
   border: 0.2rem solid transparent;
   border-radius: 50%;
   background-color: var(--color-text);
   cursor: pointer;
 }
 
 .carousel-dot.active {
  background-color: transparent;
  border: 0.2rem solid var(--color-text);
 }
</style>

