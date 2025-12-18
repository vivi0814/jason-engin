<template>
  <div class="projects-view">
    <div class="page-header">
      <div class="container">
        <h1>工程實績</h1>
        <p>展示我們在各個領域的專業實力。</p>
      </div>
    </div>

    <div class="container content-section">
      <!-- Tabs -->
      <div class="tabs">
        <button 
          :class="{ active: activeTab === 'completed' }" 
          @click="activeTab = 'completed'"
        >
          完工實績
        </button>
        <button 
          :class="{ active: activeTab === 'under-construction' }" 
          @click="activeTab = 'under-construction'"
        >
          在建工程
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="grid-3">
        <ProjectCard 
          v-for="project in filteredProjects"
          :key="project.id"
          :id="project.id"
          :title="project.title"
          :location="project.location"
          :status="project.status"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ProjectCard from '../components/ProjectCard.vue'

const activeTab = ref('completed')

const allProjects = [
  { id: 1, title: '天際線大樓', location: '市中心', status: '在建工程' },
  { id: 2, title: '河畔公寓', location: '西區', status: '完工實績' },
  { id: 3, title: '科技創新園區', location: '科技園區', status: '完工實績' },
  { id: 4, title: '綠谷購物中心', location: '北郊', status: '在建工程' },
  { id: 5, title: '市立醫院新翼', location: '醫療特區', status: '完工實績' },
  { id: 6, title: '海港大橋', location: '灣區', status: '完工實績' },
  { id: 7, title: '豪華度假村', location: '濱海區', status: '在建工程' },
  { id: 8, title: '中央圖書館', location: '市中心', status: '完工實績' }
]

const filteredProjects = computed(() => {
  if (activeTab.value === 'completed') {
    return allProjects.filter(p => p.status === '完工實績')
  } else {
    return allProjects.filter(p => p.status === '在建工程')
  }
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.page-header {
  background-color: $primary-color;
  color: $white;
  padding: 4rem 0;
  text-align: center;
  margin-bottom: 4rem;

  h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
  }

  p {
    font-size: 1.2rem;
    opacity: 0.9;
  }
}

.content-section {
  padding-bottom: 4rem;
}

.tabs {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;

  button {
    background: none;
    border: 2px solid #ddd;
    padding: 0.75rem 2rem;
    border-radius: 50px;
    font-size: 1rem;
    font-weight: 600;
    color: #666;
    cursor: pointer;
    transition: all 0.3s ease;

    &:hover {
      border-color: $secondary-color;
      color: $secondary-color;
    }

    &.active {
      background-color: $secondary-color;
      border-color: $secondary-color;
      color: $white;
    }
  }
}

.grid-3 {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;

  @media (min-width: $bp-sm) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: $bp-md) {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
