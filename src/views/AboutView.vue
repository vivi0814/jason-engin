<template>
  <div class="about-view">
    <div class="page-header">
      <div class="container">
        <h1>關於我們</h1>
        <p>以品質與誠信建立信任。</p>
      </div>
    </div>

    <div class="container content-section">
      <div class="row">
        <div class="col-text">
          <h2>我們的故事</h2>
          <p>宏圖營造成立於1990年，從一家小型在地承包商成長為區域內領先的營造公司。憑藉超過三十年的經驗，我們成功交付了數百個項目，涵蓋住宅社區到商業高樓。</p>
          <p>我們對卓越和安全的承諾贏得了客戶的信任和無數的行業獎項。我們相信，我們建造的不僅是建築，更是長久的合作關係。</p>
        </div>
        <div class="col-image">
          <div class="image-placeholder">公司形象照</div>
        </div>
      </div>

      <div class="values-section">
        <h2>核心價值</h2>
        <div class="values-grid">
          <div class="value-item">
            <h3>誠信</h3>
            <p>我們以最高的誠實和公平標準經營業務。</p>
          </div>
          <div class="value-item">
            <h3>品質</h3>
            <p>我們絕不在品質上妥協。我們使用最好的材料和工法。</p>
          </div>
          <div class="value-item">
            <h3>安全</h3>
            <p>團隊和公眾的安全是我們的首要任務。</p>
          </div>
          <div class="value-item">
            <h3>創新</h3>
            <p>我們擁抱新技術以提高效率和永續性。</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
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
    grid-template-columns: repeat(4, 1fr);
  }
}

.value-item {
  background: $white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  text-align: center;
  transition: transform 0.3s ease;

  &:hover {
    transform: translateY(-5px);
  }

  h3 {
    color: $secondary-color;
    margin-bottom: 1rem;
  }

  p {
    color: #666;
  }
}
</style>
