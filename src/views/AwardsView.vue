<template>
  <div class="awards-view">
    <div class="page-header">
      <div class="container">
        <h1>得獎紀錄</h1>
        <p>慶祝我們對卓越的承諾。</p>
      </div>
    </div>

    <div class="container content-section">
      <div class="awards-grid">
        <div class="award-item" v-for="award in awards" :key="award.id">
          <div class="award-year">{{ award.year }}</div>
          <div class="award-content">
            <h3>{{ award.title }}</h3>
            <p class="award-org">{{ award.organization }}</p>
            <p class="award-desc">{{ award.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const awards = ref([
  { id: 1, year: '2024', title: '年度最佳營造公司', organization: '全國營造業協會', description: '因在專案交付和安全標準方面的整體卓越表現而獲獎。' },
  { id: 2, year: '2023', title: '安全卓越獎', organization: '安全第一委員會', description: '表彰在所有主要工地維持零事故率。' },
  { id: 3, year: '2023', title: '綠建築創新獎', organization: '永續生活協會', description: '因在城市公園項目中採用環保材料。' },
  { id: 4, year: '2022', title: '建築傑作獎', organization: '設計與建造雜誌', description: '表彰天際線大樓獨特的設計與執行。' },
  { id: 5, year: '2021', title: '社區貢獻獎', organization: '地方政府', description: '感謝對當地基礎設施和社區發展的貢獻。' }
])
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

.awards-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  max-width: 800px;
  margin: 0 auto;
}

.award-item {
  display: flex;
  background: $white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  transition: transform 0.3s ease;
  border-left: 5px solid $secondary-color;

  &:hover {
    transform: translateX(10px);
  }

  @media (max-width: $bp-sm) {
    flex-direction: column;
  }
}

.award-year {
  font-size: 1.5rem;
  font-weight: 800;
  color: $secondary-color;
  min-width: 100px;
  margin-bottom: 1rem;

  @media (min-width: $bp-sm) {
    margin-bottom: 0;
    margin-right: 2rem;
    text-align: right;
  }
}

.award-content {
  h3 {
    color: $primary-color;
    margin-bottom: 0.5rem;
    font-size: 1.25rem;
  }

  .award-org {
    font-weight: 600;
    color: #666;
    margin-bottom: 0.5rem;
    font-size: 0.9rem;
    text-transform: uppercase;
  }

  .award-desc {
    color: #555;
    line-height: 1.6;
  }
}
</style>
