<script setup>
defineProps({
    project: Object
})
</script>

<template>
  <article class="project-card">
    <div class="content">
      <h2 class="project-card__title">{{ project.title }}</h2>
      <p class="project-card__category">{{ project.category }}</p>
      <div class="project-card__image">
         <img :src="project.imageUrl" :alt="project.title">
      </div>
      <slot name="carousel"></slot>
      <p class="project-card__description">{{ project.description }}</p>
    </div>
  </article>
</template>

<style scoped>
.project-card {
  background-color: var(--color-card);
  color: var(--color-text);
  font-family: var(--font-primary);

}

.project-card__title {
  font-size: var(--font-size-title);
}

.project-card__category {
  font-size: var(--font-size-category);
  background-color: var(--color-background);
  color: var(--color-category);
  width: fit-content;
  padding: 0.15rem;
  border-radius: 0.2rem;
  margin-bottom: 0.5rem;
  line-height: 1.1;
}

.project-card__description {
  font-size: var(--font-size-body);
}

.content {
  padding-inline: var(--content-padding);
}

.project-card__image {
  width: 100%;
  height: 35rem;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}

.project-card__image img {
  max-width: 100%;
  max-height: 100%;
  width: auto;
  height: auto;
  object-fit: contain;
}
</style>
