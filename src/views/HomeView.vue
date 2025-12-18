<template>
  <div class="home-view">
    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content container">
        <h1>打造未來 <br><span class="highlight">追求卓越</span></h1>
        <p>自1990年以來，領先業界的營造公司，致力於提供高品質的工程項目。</p>
        <div class="hero-actions">
          <RouterLink to="/projects" class="btn btn-primary">瀏覽工程實績</RouterLink>
          <RouterLink to="/contact" class="btn btn-outline">聯絡我們</RouterLink>
        </div>
      </div>
    </section>

    <!-- Latest News -->
    <section class="section news-section">
      <div class="container">
        <div class="section-header">
          <h2>最新消息</h2>
          <RouterLink to="/" class="view-all">查看所有消息</RouterLink>
        </div>
        <div class="grid-3">
          <NewsCard 
            v-for="item in newsItems" 
            :key="item.id"
            :id="item.id"
            :date="item.date"
            :title="item.title"
            :summary="item.summary"
          />
        </div>
      </div>
    </section>

    <!-- Featured Projects -->
    <section class="section bg-light">
      <div class="container">
        <div class="section-header">
          <h2>精選工程</h2>
          <RouterLink to="/projects" class="view-all">查看所有工程</RouterLink>
        </div>
        <div class="grid-3">
          <ProjectCard 
            v-for="project in featuredProjects"
            :key="project.id"
            :id="project.id"
            :title="project.title"
            :location="project.location"
            :status="project.status"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import NewsCard from '../components/NewsCard.vue'
import ProjectCard from '../components/ProjectCard.vue'

const newsItems = ref([
  { id: 1, date: '2024年12月15日', title: '榮獲2024年度最佳營造公司殊榮', summary: '我們很榮幸因在工程品質與安全標準上的卓越表現，獲得此項殊榮。' },
  { id: 2, date: '2024年11月20日', title: '全新環保辦公大樓動工', summary: '位於市中心的全新永續辦公大樓正式動土，該項目將致力於取得LEED白金級認證。' },
  { id: 3, date: '2024年10月05日', title: '城市大橋工程順利完工', summary: '主要的城市基礎設施項目提前完工，大幅改善了城市的交通連結。' }
])

const featuredProjects = ref([
  { id: 1, title: '天際線大樓', location: '市中心', status: '在建工程' },
  { id: 2, title: '河畔公寓', location: '西區', status: '完工實績' },
  { id: 3, title: '科技創新園區', location: '科技園區', status: '完工實績' }
])
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.hero {
  background: linear-gradient(rgba(0, 51, 102, 0.8), rgba(0, 51, 102, 0.8)), url('https://placehold.co/1920x1080/003366/FFFFFF/png?text=Construction+Site') no-repeat center center;
  background-size: cover;
  color: $white;
  padding: 8rem 0;
  text-align: center;

  h1 {
    font-size: 2.5rem;
    font-weight: 800;
    margin-bottom: 1.5rem;
    line-height: 1.2;

    @media (min-width: $bp-sm) {
      font-size: 3.5rem;
    }

    .highlight {
      color: $secondary-color;
    }
  }

  p {
    font-size: 1.1rem;
    max-width: 600px;
    margin: 0 auto 2.5rem;
    opacity: 0.9;
  }
}

.hero-actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
}

.btn {
  display: inline-block;
  padding: 0.8rem 1rem;
  border-radius: 4px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  cursor: pointer;

  &.btn-primary {
    background-color: $secondary-color;
    color: $white;
    border: 2px solid $secondary-color;

    &:hover {
      background-color: darken($secondary-color, 10%);
      border-color: darken($secondary-color, 10%);
    }
  }

  &.btn-outline {
    background-color: transparent;
    color: $white;
    border: 2px solid $white;

    &:hover {
      background-color: $white;
      color: $primary-color;
    }
  }
}

.section {
  padding: 5rem 0;

  &.bg-light {
    background-color: #f0f2f5;
  }
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 3rem;
  border-bottom: 2px solid #eee;
  padding-bottom: 1rem;

  h2 {
    font-size: 2rem;
    color: $primary-color;
    position: relative;

    &::after {
      content: '';
      position: absolute;
      bottom: -1.1rem;
      left: 0;
      width: 60px;
      height: 3px;
      background-color: $secondary-color;
    }
  }

  .view-all {
    color: $secondary-color;
    font-weight: 600;
    
    &:hover {
      text-decoration: underline;
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
