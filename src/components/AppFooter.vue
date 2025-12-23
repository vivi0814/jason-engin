<template>
  <footer class="app-footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>傑昇營造股份有限公司</h3>
          <p>傑昇營造股份有限公司</p>
          <p>JASON ENGINEERING CO.,LTD</p>
          <p>傑元建設股份有限公司</p>
          <p>JAYUAN CONSTRUCTION CO.,LTD</p>
        </div>
        <div class="footer-section">
          <h4>聯絡資訊</h4>
          <p>新北市板橋區館前西路6號7樓</p>
          <p>電話: (02)8952-3999</p>
          <p>Email: jason.apply@msa.hinet.net</p>
        </div>
        <div class="footer-section">
          <h4>快速連結</h4>
          <ul>
            <li><RouterLink to="/projects">工程實績</RouterLink></li>
            <li><RouterLink to="/contact">聯絡我們</RouterLink></li>
          </ul>
        </div>
      </div>
      <div class="copyright">
        &copy; {{ new Date().getFullYear() }} 傑昇營造. All rights reserved.
      </div>
    </div>
  </footer>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.app-footer {
  background-color: $primary-color;
  color: $white;
  padding: 3rem 0 1rem;
  margin-top: auto;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-section {
  h3 {
    color: $secondary-color;
    margin-bottom: 1rem;
  }

  h4 {
    color: $secondary-color;
    margin-bottom: 0.5rem;
  }

  ul {
    li {
      margin-bottom: 0.5rem;
    }
  }

  a {
    color: $white;
    opacity: 0.8;
    &:hover {
      opacity: 1;
      color: $secondary-color;
    }
  }
}

.copyright {
  text-align: center;
  padding-top: 1rem;
  border-top: 1px solid rgba(255,255,255,0.1);
  font-size: 0.9rem;
  opacity: 0.7;
}
</style>
