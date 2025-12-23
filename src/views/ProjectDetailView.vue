<template>
  <div class="project-detail-view">
    <div class="container">
      <div class="back-link">
        <RouterLink to="/projects">&larr; 返回工程實績</RouterLink>
      </div>

      <article v-if="project" class="project-content">
        <div class="project-header">
          <div class="header-info">
            <span class="status" :class="project.status === '完工實績' ? 'completed' : 'under-construction'">{{ project.status }}</span>
            <h1>{{ project.title }}</h1>
            <p class="location"><span class="icon">📍</span> {{ project.location }}</p>
          </div>
        </div>

        <div class="project-main-content">
          <div class="project-description">
            <h2>專案介紹</h2>
            <p class="description-text" v-if="project.description">{{ project.description }}</p>
            <p v-else>這是關於 <strong>{{ project.title }}</strong> 的詳細介紹。此項目位於 {{ project.location }}，是我們公司的重點工程之一。</p>
          </div>

          <div class="project-gallery">
            <div class="main-image">
              <img v-if="project.image" :src="project.image" :alt="project.title">
              <div v-else class="placeholder-img">專案主圖</div>
            </div>
          </div>
        </div>
      </article>

      <div v-else class="not-found">
        <p>找不到該工程項目。</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { allProjects } from '../data/projects'

const route = useRoute()
const project = ref(null)

onMounted(() => {
  const id = parseInt(route.params.id)
  project.value = allProjects.find(p => p.id === id)
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.project-detail-view {
  padding: 4rem 0;
}

.back-link {
  margin-bottom: 2rem;
  
  a {
    color: $secondary-color;
    font-weight: 600;
    
    &:hover {
      text-decoration: underline;
    }
  }
}

.project-content {
  background: $white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0,0,0,0.05);
}

.project-header {
  padding: 2rem;
  border-bottom: 1px solid #eee;
  background-color: #fafafa;

  .status {
    display: inline-block;
    padding: 0.25rem 0.75rem;
    border-radius: 50px;
    font-size: 0.8rem;
    font-weight: 600;
    margin-bottom: 1rem;
    
    &.completed {
      background-color: rgba($primary-color, 0.1);
      color: $primary-color;
    }

    &.under-construction {
      background-color: rgba($secondary-color, 0.1);
      color: darken($secondary-color, 10%);
    }
  }

  h1 {
    font-size: 2rem;
    color: $primary-color;
    margin-bottom: 0.5rem;
    
    @media (min-width: $bp-sm) {
      font-size: 2.5rem;
    }
  }

  .location {
    color: #666;
    font-size: 1.1rem;
  }
}

.project-main-content {
  display: flex;
  flex-direction: column;
  padding: 2rem;
  gap: 2rem;

  @media (min-width: $bp-md) {
    flex-direction: row;
    align-items: flex-start;
  }
}

.project-description {
  flex: 1;

  h2 {
    color: $primary-color;
    margin-bottom: 1.5rem;
    font-size: 1.8rem;
    position: relative;
    padding-bottom: 0.5rem;

    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 40px;
      height: 3px;
      background-color: $secondary-color;
    }
  }

  .description-text {
    line-height: 1.8;
    color: #444;
    font-size: 1.1rem;
    white-space: pre-line;
  }
}

.project-gallery {
  width: 100%;
  
  @media (min-width: $bp-md) {
    width: 40%;
    position: sticky;
    top: 100px;
  }
  
  .main-image {
    width: 100%;
    aspect-ratio: 4 / 3;
    background-color: #f0f0f0;
    border-radius: 4px;
    overflow: hidden;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .placeholder-img {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      background: linear-gradient(45deg, $primary-color, lighten($primary-color, 20%));
      color: rgba(255,255,255,0.5);
      font-size: 1.5rem;
      font-weight: 700;
    }
  }
}
</style>
