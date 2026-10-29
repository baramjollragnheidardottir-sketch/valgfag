<script setup>
import { ref } from 'vue'

defineProps({
    projects: Array
})

const emit = defineEmits(['projectSaved'])
const title = ref('')
const category = ref('')
const imageUrl = ref('')
const description = ref('')

const saveProject = () => {
    const newProject = {
        title: title.value,
        category: category.value,
        imageUrl: imageUrl.value,
        description: description.value
    }

const url = 'https://valgfag-9c07e-default-rtdb.europe-west1.firebasedatabase.app/myProject.json'

    fetch(url, {
        method: 'PUT',
        headers: {
            'content-type': 'application/json'
        },
        body: JSON.stringify(newProject)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('Failed to save project')
        }
        
        console.log('Project saved successfully')
        emit('projectSaved', newProject)
        title.value = ''
        category.value = ''
        imageUrl.value = ''
        description.value = ''
    })
    .catch(error => {
        console.error('Error saving project:', error)
    })
}

</script>

<template>
 <form class="project-form" @submit.prevent="saveProject">

    <label for="title" class="visually-hidden">
        Project title
    </label>
    <input 
    class="project-form__title"
    type="text" 
    id="title" 
    name="title" 
    v-model="title"
    placeholder="Write your project title here!"
    required 
    />

    <label for ="category" class="visually-hidden">
        Project category
    </label>
    <input 
    class="project-form__category"
    type="text" 
    id="category" 
    name="category" 
    v-model="category"
    placeholder="Write your project category here!"
    required 
    />
    
    <label for="imageUrl" class="visually-hidden">
        Project image
    </label>

    <select
    class="project-form__image-select"
    id="imageUrl"
    name="imageUrl"
    v-model="imageUrl"
    required
    >
   <option value="" disabled>Choose your image</option>

    <option
    v-for="project in projects"
    :key="project.imageUrl"
    :value="project.imageUrl"
    >
    {{ project.title }}
   </option>
   </select>

    <div class="project-form__image">
    <img
    v-if="imageUrl"
    :src="imageUrl"
    :alt="title || 'Selected project image'"
    >
    </div>

    <label for="description" class="visually-hidden">
        Project description
    </label>
    <textarea 
    class="project-form__description"
    id="description" name="description" 
    v-model="description"
    placeholder="Write your project description here!" 
    required></textarea>

    <button type="submit">Save your new project!</button>
 </form>
</template>

<style scoped>
.project-form {
  background-color: var(--color-card);
  color: var(--color-text);
  font-family: var(--font-primary);
  padding-inline: var(--content-padding);
}

.project-form__title {
  display: block;
  width: 100%;
  font-family: var(--font-primary);
  font-size: var(--font-size-title);
  color: var(--color-text);
  background: transparent;
  border: none;
  padding: 0;
}

.project-form__title::placeholder {
  color: var(--color-text);
  opacity: 1;
}

.project-form__category {
  display: block;
  width: auto;
  field-sizing: content;
  max-width: 100%;
  font-family: var(--font-primary);
  font-size: var(--font-size-category);
  background-color: var(--color-background);
  color: var(--color-category);
  border: none;
  border-radius: 0.2rem;
  padding: 0.15rem;
  line-height: 1.1;
  margin-bottom: 0.5rem;
}

.project-form__category::placeholder {
  color: var(--color-category);
  opacity: 1;
}

.project-form__category:focus {
  background-color: var(--color-background);
  color: var(--color-category);
}

.project-form__category:-webkit-autofill {
  -webkit-text-fill-color: var(--color-category);
  box-shadow: 0 0 0 1000px var(--color-background) inset;
}

.project-form__description {
  display: block;
  width: 100%;
  font-family: var(--font-primary);
  font-size: var(--font-size-body);
  color: var(--color-text);
  background: transparent;
  border: none;
  padding: 0;
  resize: none;
  field-sizing: content;
  min-height: 3rem;
}

.project-form__description::placeholder {
  color: var(--color-text);
  opacity: 1;
}

.project-form__image {
  width: 100%;
  height: 35rem;
  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.project-form__image img {
  max-width: 100%;
  max-height: 100%;
  width: auto;
  height: auto;
  object-fit: contain;
}

.project-form__image-select {
  display: block;
  width: fit-content;
  max-width: 100%;
  font-family: var(--font-primary);
  font-size: var(--font-size-category);
  color: var(--color-category);
  background-color: var(--color-background);
  border: none;
  border-radius: 0.2rem;
  padding: 0.15rem;
  line-height: 1.1;
  margin-bottom: 0.5rem;
  cursor: pointer;
}

.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
  border: 0;
}

</style>