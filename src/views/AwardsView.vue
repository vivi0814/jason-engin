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
          <div class="award-img">
            <img :src="award.image" alt="Award Image">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const awards = ref([
  { id: 1, year: '2007',
    title: '2007年榮獲 國家建築金質獎',
    organization: '中華民國國家企業競爭力發展協會',
    description: '憑藉工程品質、施工安全與專案管理之整體表現獲得肯定，展現公司在營造專業上的卓越實力。',
    image: '/images/award1.jpg' },
  { id: 2, year: '2007',
    title: '2007年榮獲 國家優良營造商認證',
    organization: '中華民國國家企業競爭力發展協會',
    description: '在多項工程專案中落實工地安全管理制度，維持良好施工紀錄，獲頒國家級營造品質認證。',
    image: '/images/award2.jpg' },
  { id: 3, year: '2007',
    title: '七堵國小感謝狀',
    organization: '地方政府',
    description: '感謝對當地基礎設施和社區發展的貢獻。',
    image: '/images/award3.jpg' },
  { id: 4, year: '2008',
    title: '2008年榮獲 中華建築金石獎',
    organization: '中華建築金石獎活動委員會',
    description: '於工程設計整合與施工執行層面表現優異，兼顧結構安全與整體美感，獲建築專業評審肯定。',
    image: '/images/award4.jpg' },
  { id: 5, year: '2008',
    title: '福星國小感謝狀',
    organization: '地方政府',
    description: '感謝對當地基礎設施和社區發展的貢獻。',
    image: '/images/award5.jpg' },
  { id: 6, year: '2008',
    title: '七堵國小感謝狀',
    organization: '地方政府',
    description: '感謝對當地基礎設施和社區發展的貢獻。',
    image: '/images/award6.jpg' },
  { id: 7, year: '2008',
    title: '榮富國小感謝狀',
    organization: '地方政府',
    description: '感謝對當地基礎設施和社區發展的貢獻。',
    image: '/images/award7.jpg' },
  { id: 8, year: '2008',
    title: '德育技術學院感謝狀',
    organization: '地方政府',
    description: '感謝對當地基礎設施和社區發展的貢獻。',
    image: '/images/award8.jpg' }
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
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  transition: transform 0.3s ease;
  border-left: 5px solid $secondary-color;
  gap: 1rem;

  &:hover {
    transform: translateX(10px);
  }

  @media (max-width: 639px) {
    flex-direction: column;
    max-height: none;
    width: 100%;
    margin: 0 auto;
    gap: 0;
  }

  @media (min-width: $bp-sm) {
    max-height: 200px;
  }
}

.award-year {
  padding: 1rem;
  font-size: 1.5rem;
  font-weight: 800;
  color: $secondary-color;
  min-width: 100px;

  @media (max-width: 639px) {
    order: 1;
    margin-bottom: 0.5rem;
    padding: 0 0 0 1rem;
  }

  @media (min-width: $bp-sm) {
    text-align: right;
    padding: 0.5rem;
  }
}

.award-content {
  padding: 1rem;
  flex: 1;

  @media (max-width: 639px) {
    order: 2;
    max-width: none;
    padding: 0 0 1rem 1rem;
  }

  @media (min-width: $bp-sm) {
    max-width: 450px;
    padding: 0.5rem;
  }

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

.award-img {
  @media (max-width: 639px) {
    order: 3;
    max-width: 100%;
    max-height: 200px;
    margin-left: 0;
    img{
      object-fit: contain;
    }
  }

  @media (min-width: $bp-sm) {
    max-width: 200px;
    max-height: 200px;
    margin-left: auto;
    img {
      object-fit: cover;
    }
  }

  img {
    width: 100%;
    height: 100%;
  }
}
</style>
