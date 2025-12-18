<template>
  <div class="news-detail-view">
    <div class="container">
      <div class="back-link">
        <RouterLink to="/">&larr; 返回首頁</RouterLink>
      </div>
      
      <article v-if="newsItem" class="news-content">
        <div class="news-header">
          <span class="date">{{ newsItem.date }}</span>
          <h1>{{ newsItem.title }}</h1>
        </div>
        <div class="news-body">
          <p class="summary">{{ newsItem.summary }}</p>
          <div class="content-placeholder">
            <p>這裡將顯示完整的新聞內容...</p>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
            <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
          </div>
        </div>
      </article>
      
      <div v-else class="not-found">
        <p>找不到該則新聞。</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const newsItem = ref(null)

// Mock data - in a real app this would come from an API or store
const allNews = [
  { id: 1, date: '2024年12月15日', title: '榮獲2024年度最佳營造公司殊榮', summary: '我們很榮幸因在工程品質與安全標準上的卓越表現，獲得此項殊榮。' },
  { id: 2, date: '2024年11月20日', title: '全新環保辦公大樓動工', summary: '位於市中心的全新永續辦公大樓正式動土，該項目將致力於取得LEED白金級認證。' },
  { id: 3, date: '2024年10月05日', title: '城市大橋工程順利完工', summary: '主要的城市基礎設施項目提前完工，大幅改善了城市的交通連結。' }
]

onMounted(() => {
  const id = parseInt(route.params.id)
  newsItem.value = allNews.find(item => item.id === id)
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.news-detail-view {
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

.news-content {
  background: $white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.05);
}

.news-header {
  margin-bottom: 2rem;
  border-bottom: 1px solid #eee;
  padding-bottom: 1rem;

  .date {
    display: block;
    color: #666;
    margin-bottom: 0.5rem;
    font-size: 0.9rem;
  }

  h1 {
    color: $primary-color;
    font-size: 2rem;
  }
}

.news-body {
  .summary {
    font-size: 1.2rem;
    font-weight: 500;
    color: #333;
    margin-bottom: 2rem;
    line-height: 1.6;
  }

  .content-placeholder {
    color: #555;
    line-height: 1.8;
    
    p {
      margin-bottom: 1rem;
    }
  }
}
</style>
