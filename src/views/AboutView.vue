<template>
  <div class="about-view">
    <div class="page-header">
      <div class="container">
        <h1>關於我們</h1>
        <p>家的築夢者、築夢的專家</p>
      </div>
    </div>

    <div class="container content-section">
      <!-- 公司概況 / 主敘述 -->
      <div class="row">
        <div class="col-text">
          <h2>企業概況</h2>
          <p>長久的品質堅持，造就今日的品牌價值 ─ 關於傑昇營造</p>
          <p>創造建築的表情，豐富生活的感情 ─ 關於傑元建設</p>
        </div>

        <div class="col-image">
          <div class="image-placeholder">公司形象照 / 公司實景</div>
        </div>
      </div>

      <!-- 經營理念區塊 -->
      <div class="values-section">
        <h2>經營理念與願景</h2>

        <div class="values-grid">
          <div
            v-for="item in principles"
            :key="item.title"
            class="value-item"
          >
            <h3>{{ item.title }}</h3>
            <p class="value-subtitle" v-if="item.subtitle">{{ item.subtitle }}</p>
            <p>{{ item.desc }}</p>
          </div>
        </div>
      </div>

      <!-- 收穫 -->
      <div class="harvest-section">
        <h2>收穫</h2>
        <p>肯定除了是榮譽，更是創新的動力，進步的壓力</p>
      </div>

      <!-- 公司實景（你之後可以換成圖片牆） -->
      <!-- <div class="gallery-section">
        <h2>公司實景</h2>
        <div class="gallery-placeholder">（可放照片牆 / 輪播 / 圖片格）</div>
      </div> -->
    </div>
  </div>
</template>

<script setup>
const principles = [
  {
    title: '經營倫理',
    desc: '以正直與負責的態度面對每一項工程，堅守專業與誠信，建立長久信任。'
  },
  {
    title: '經營理念',
    desc: '傑昇營造以20年歲月，累積對建築事業的追求與理想。'
  },
  {
    title: '經營願景',
    desc: '企業永續經營，不僅是良心，更是責任。'
  },
  {
    title: '誠信服務',
    desc: '始終如一的用心堅持，締造「零客訴」的服務最高境界。'
  },
  {
    title: '工程管理',
    desc: '周詳的規劃，嚴謹的施工，無可妥協的品質。'
  },
  {
    title: '公司團隊',
    desc: '用對的人，做對的事，教育、訓練與團隊學習。'
  }
]
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

.row {
  display: flex;
  flex-direction: column;
  gap: 3rem;
  margin-bottom: 5rem;

  @media (min-width: $bp-md) {
    flex-direction: row;
    align-items: center;
  }
}

.col-text {
  flex: 1;

  h2 {
    color: $primary-color;
    margin-bottom: 1.5rem;
    font-size: 2rem;
  }

  p {
    margin-bottom: 1rem;
    font-size: 1.1rem;
    color: #555;
  }
}

.col-image {
  flex: 1;

  .image-placeholder {
    width: 100%;
    height: 300px;
    background-color: #eee;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #999;
    font-weight: 600;
    border-radius: 8px;
  }
}

.values-section {
  h2 {
    text-align: center;
    color: $primary-color;
    margin-bottom: 3rem;
    font-size: 2rem;
  }
}

.values-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;

  @media (min-width: $bp-sm) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: $bp-lg) {
    grid-template-columns: repeat(3, 1fr);
  }
}

.value-item {
  background: $white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  text-align: center;
  transition: transform 0.3s ease;

  &:hover {
    transform: translateY(-5px);
  }

  h3 {
    color: $secondary-color;
    margin-bottom: 0.75rem;
  }

  .value-subtitle {
    font-weight: 700;
    color: $primary-color;
    margin-bottom: 0.75rem;
  }

  p {
    color: #666;
    line-height: 1.7;
  }
}

.harvest-section,
.gallery-section {
  margin-top: 5rem;

  h2 {
    text-align: center;
    color: $primary-color;
    margin-bottom: 1.5rem;
    font-size: 2rem;
  }

  p {
    text-align: center;
    color: #555;
    font-size: 1.1rem;
  }
}

.gallery-placeholder {
  margin-top: 2rem;
  height: 220px;
  border-radius: 8px;
  background: #f3f3f3;
  color: #999;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
}
</style>
