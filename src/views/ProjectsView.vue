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
          v-for="project in paginatedProjects"
          :key="project.id"
          :id="project.id"
          :title="project.title"
          :location="project.location"
          :status="project.status"
          :image="project.image"
        />
      </div>

      <!-- Pagination -->
      <div v-if="totalPages > 1" class="pagination">
        <button 
          class="page-btn" 
          :disabled="currentPage === 1"
          @click="currentPage--"
        >
          &laquo; 上一頁
        </button>
        
        <div class="page-numbers">
          <button 
            v-for="page in totalPages" 
            :key="page"
            class="page-number"
            :class="{ active: currentPage === page }"
            @click="currentPage = page"
          >
            {{ page }}
          </button>
        </div>

        <button 
          class="page-btn" 
          :disabled="currentPage === totalPages"
          @click="currentPage++"
        >
          下一頁 &raquo;
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import ProjectCard from '../components/ProjectCard.vue'
import { allProjects } from '../data/projects'

const activeTab = ref('completed')
const currentPage = ref(1)
const itemsPerPage = 9

// Reset pagination when tab changes
watch(activeTab, () => {
  currentPage.value = 1
})

const filteredProjects = computed(() => {
  if (activeTab.value === 'completed') {
    return allProjects.filter(p => p.status === '完工實績')
  } else {
    return allProjects.filter(p => p.status === '在建工程')
  }
})

const totalPages = computed(() => {
  return Math.ceil(filteredProjects.value.length / itemsPerPage)
})

const paginatedProjects = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage
  const end = start + itemsPerPage
  return filteredProjects.value.slice(start, end)
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
  margin-bottom: 3rem;

  @media (min-width: $bp-sm) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: $bp-md) {
    grid-template-columns: repeat(3, 1fr);
  }
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  margin-top: 2rem;

  .page-numbers {
    display: flex;
    gap: 0.5rem;
  }

  .page-btn, .page-number {
    background: $white;
    border: 1px solid #ddd;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    font-weight: 600;
    color: #666;
    cursor: pointer;
    transition: all 0.3s ease;

    &:hover:not(:disabled) {
      border-color: $secondary-color;
      color: $secondary-color;
    }

    &:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    &.active {
      background-color: $secondary-color;
      border-color: $secondary-color;
      color: $white;
    }
  }

  @media (max-width: 639px) {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
