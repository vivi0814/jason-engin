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

        <div v-if="newsItem.image" class="news-image">
          <img :src="newsItem.image" :alt="newsItem.title">
        </div>

        <div class="news-body">
          <p class="summary">{{ newsItem.summary }}</p>
          <div class="content-placeholder">
            <p>{{ newsItem.description1 }}</p>
            <p>{{ newsItem.description2 }}</p>
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
  { 
    id: 1, 
    date: '2010年11月19日', 
    title: '榮獲第十六屆中華建築金石獎', 
    summary: '傑昇榮獲第十六屆中華建築金石獎，與總統召見留影',
    image: '/images/news1.jpg',
    description1: '本公司秉持「安全、品質、誠信」的核心理念，長期深耕營造專業，從工程規劃、施工管理到品質檢核，皆以最高標準自我要求。此次榮獲 金石獎，不僅是對團隊專業實力與工程品質的高度肯定，更是對我們多年來堅持細節、落實責任的最佳證明。',
    description2: '我們深信，優質的工程不只是建築的完成，更是對使用者安全、城市環境與社會責任的承諾。未來，本公司將持續精進技術、深化管理，以更嚴謹的態度與創新的思維，為每一項工程注入長久價值，成為值得信賴的營造夥伴。'
  },
  { 
    id: 2, 
    date: '2010年11月18日', 
    title: '六本木新建工程榮獲金石獎', 
    summary: '衣蝶六本木新建工程榮獲第十六屆中華建築金石獎優良施工品質（住宅中層組）',
    image: '/images/news2.jpg',
    description1:'衣蝶六本木新建工程在施工過程中，秉持嚴謹的工程管理制度與高標準的品質控管，從結構安全、工法細節到施工流程皆確實落實規範要求，展現住宅工程應有的專業水準與穩定品質。全案施工期間，團隊以完善的工序規劃與細節管理，確保工程品質一致性，為住戶打造安全、耐久且兼具品質的居住空間。',
    description2: '憑藉卓越的施工品質與完整的管理成果，本案榮獲**第十六屆中華建築金石獎—優良施工品質（住宅中層組）**肯定。此次獲獎不僅是對單一工程成果的肯定，更象徵本公司長期深耕住宅工程、持續精進施工技術與品質管理的具體成果，未來亦將以同樣嚴謹的態度，持續為每一項工程創造值得信賴的價值。',
    
  },
  { 
    id: 3, 
    date: '2010年11月04日', 
    title: '榮獲第九屆國家建築金質獎', 
    summary: '傑昇榮獲第九屆國家建築金質獎，與總統召見留影',
    image: '/images/news3.jpg',
    description1:'傑昇以卓越的工程品質、嚴謹的施工管理與對建築安全的高度承諾，榮獲第九屆國家建築金質獎肯定，展現團隊在建築專業領域長期深耕的成果與實力。此次獲獎，不僅象徵對工程品質與技術水準的高度認可，更彰顯傑昇持續追求卓越、落實責任施工的核心價值。',
    description2: '頒獎典禮中，傑昇代表受邀與總統召見並合影留念，為本次榮耀留下重要里程碑。這份肯定不僅是對企業團隊努力的嘉勉，更是一份對社會與公共安全的責任期許。未來，傑昇將持續以最高標準自我要求，精進專業技術，為建築品質與城市發展貢獻長久而穩健的力量。',
  },
  { 
    id: 4, 
    date: '2010年11月04日', 
    title: '榮獲國家優良營造商認證標章', 
    summary: '榮獲國家優良營造商認證標章-呂副總統頒獎',
    image: '/images/news4.jpg',
    description1:'本公司長期秉持「安全第一、品質至上、誠信負責」的經營理念，於工程管理、施工品質與職業安全等面向皆持續精進，榮獲國家優良營造商認證標章肯定。此項認證象徵對企業整體營運制度、工程品質與專業能力的高度認可，亦是團隊多年來落實責任施工與品質管理的具體成果。',
    description2: '頒獎典禮中，由呂副總統親自頒獎，為本次榮耀賦予更深層的意義。這份肯定不僅是對過往努力的肯定，更是一份持續精進的責任與期許。未來，本公司將持續以更嚴謹的態度精進技術與管理，守護工程品質與公共安全，成為社會大眾值得信賴的營造夥伴。',
  },
  { 
    id: 5, 
    date: '2010年11月04日', 
    title: '榮獲國家優良營造商認證標章', 
    summary: '榮獲國家優良營造商認證標章-鍾榮吉副院長頒獎',
    image: '/images/news5.jpg',
    description1:'本公司長期秉持嚴謹的工程管理制度與高標準施工品質，於工程安全、品質控管及企業治理等面向皆展現穩定且成熟的專業能力，榮獲國家優良營造商認證標章肯定。此項認證象徵對企業整體營運體質與施工品質的高度認可，也是團隊持續落實責任施工與專業精進的重要成果。',
    description2: '頒獎典禮中，由鍾榮吉副院長親自頒獎，為本次榮耀留下珍貴紀錄。這份肯定不僅是對企業專業實力的再度認可，更是一份對未來持續守護工程品質與公共安全的期許。本公司將持續以嚴謹的態度精進技術與管理，穩健承擔每一項工程責任，為社會創造長久而可靠的價值。',
  }
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
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
  max-width: 900px;
  margin: 0 auto;
}

.news-header {
  margin-bottom: 2rem;
  text-align: center;

  .date {
    display: inline-block;
    background: rgba($secondary-color, 0.1);
    color: $secondary-color;
    padding: 0.2rem 1rem;
    border-radius: 20px;
    margin-bottom: 1rem;
    font-size: 0.9rem;
    font-weight: 600;
  }

  h1 {
    color: $primary-color;
    font-size: 2.2rem;
    line-height: 1.3;
  }
}

.news-image {
  margin: 2rem -2rem;
  
  img {
    width: 100%;
    height: auto;
    display: block;
  }

  @media (max-width: 639px) {
    margin: 2rem -1rem;
  }
}

.news-body {
  .summary {
    font-size: 1.25rem;
    font-weight: 500;
    color: #333;
    margin-bottom: 2rem;
    line-height: 1.8;
    border-left: 4px solid $secondary-color;
    padding-left: 1.5rem;
  }

  .content-placeholder {
    color: #555;
    line-height: 1.8;
    font-size: 1.1rem;
    
    p {
      margin-bottom: 1.5rem;
    }
  }
}
</style>
