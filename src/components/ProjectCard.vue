<template>
  <RouterLink :to="`/projects/${id}`" class="project-card">
    <div class="project-image">
      <img v-if="image" :src="image" :alt="title">
      <div v-else class="placeholder-img"></div>
    </div>
    <div class="project-info">
      <span class="project-status" :class="status === '完工實績' ? 'completed' : 'under-construction'">{{ status }}</span>
      <h3 class="project-title">{{ title }}</h3>
      <p class="project-location">{{ location }}</p>
    </div>
  </RouterLink>
</template>

<script setup>
import { RouterLink } from 'vue-router'

defineProps({
  id: Number,
  title: String,
  location: String,
  status: String, // 'Completed' or 'Under Construction'
  image: String
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.project-card {
  background: $white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  transition: transform 0.3s ease;

  &:hover {
    transform: translateY(-5px);
    
    .placeholder-img, img {
      transform: scale(1.05);
    }
  }
}

.project-image {
  height: 200px;
  overflow: hidden;
  background-color: #eee;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
}

.placeholder-img {
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, $primary-color, lighten($primary-color, 20%));
  transition: transform 0.5s ease;
}

.project-info {
  padding: 1.5rem;
}

.project-status {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  border-radius: 50px;
  font-size: 0.75rem;
  font-weight: 600;
  margin-bottom: 0.75rem;
  text-transform: uppercase;

  &.completed {
    background-color: rgba($primary-color, 0.1);
    color: $primary-color;
  }

  &.under-construction {
    background-color: rgba($secondary-color, 0.1);
    color: darken($secondary-color, 10%);
  }
}

.project-title {
  font-size: 1.25rem;
  color: $text-color;
  margin-bottom: 0.5rem;
}

.project-location {
  font-size: 0.9rem;
  color: #666;
}
</style>
