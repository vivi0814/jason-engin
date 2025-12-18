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

        <div class="project-gallery">
          <div class="main-image">
            <div class="placeholder-img">專案主圖</div>
          </div>
        </div>

        <div class="project-description">
          <h2>專案介紹</h2>
          <p>這是關於 <strong>{{ project.title }}</strong> 的詳細介紹。此項目位於 {{ project.location }}，是我們公司的重點工程之一。</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus lacinia odio vitae vestibulum vestibulum. Cras venenatis euismod malesuada. Nullam ac odio tenus et.</p>
          
          <h3>工程亮點</h3>
          <ul>
            <li>採用最新環保建材</li>
            <li>抗震係數達 0.4g</li>
            <li>智慧建築管理系統</li>
          </ul>
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

const route = useRoute()
const project = ref(null)

// Mock data - same as ProjectsView
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
    font-size: 2.5rem;
    color: $primary-color;
    margin-bottom: 0.5rem;
  }

  .location {
    color: #666;
    font-size: 1.1rem;
  }
}

.project-gallery {
  height: 400px;
  background-color: #f0f0f0;
  
  .main-image {
    width: 100%;
    height: 100%;
    
    .placeholder-img {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      background: linear-gradient(45deg, $primary-color, lighten($primary-color, 20%));
      color: rgba(255,255,255,0.5);
      font-size: 2rem;
      font-weight: 700;
    }
  }
}

.project-description {
  padding: 2rem;

  h2 {
    color: $primary-color;
    margin-bottom: 1rem;
  }

  h3 {
    color: $secondary-color;
    margin: 1.5rem 0 1rem;
  }

  p {
    margin-bottom: 1rem;
    line-height: 1.6;
    color: #444;
  }

  ul {
    list-style: disc;
    padding-left: 1.5rem;
    
    li {
      margin-bottom: 0.5rem;
      color: #555;
    }
  }
}
</style>
