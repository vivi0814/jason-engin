<template>
  <header class="app-header">
    <div class="container header-content">
      <div class="logo">
        <RouterLink to="/"><img src="/images/logo.png" alt="logo"></RouterLink>
      </div>
      
      <button class="menu-toggle" @click="isMenuOpen = !isMenuOpen" :aria-expanded="isMenuOpen" aria-label="Toggle navigation">
        <span class="hamburger"></span>
      </button>

      <nav :class="{ 'is-open': isMenuOpen }">
        <ul>
          <li><RouterLink to="/" @click="isMenuOpen = false">最新消息</RouterLink></li>
          <li><RouterLink to="/about" @click="isMenuOpen = false">關於我們</RouterLink></li>
          <li><RouterLink to="/projects" @click="isMenuOpen = false">工程實績</RouterLink></li>
          <li><RouterLink to="/awards" @click="isMenuOpen = false">得獎紀錄</RouterLink></li>
          <li><RouterLink to="/contact" @click="isMenuOpen = false">聯絡我們</RouterLink></li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { RouterLink } from 'vue-router'

const isMenuOpen = ref(false)

const checkScreenSize = () => {
  if (window.innerWidth >= 960) { // $bp-md
    isMenuOpen.value = false
  }
}

onMounted(() => {
  window.addEventListener('resize', checkScreenSize)
})

onUnmounted(() => {
  window.removeEventListener('resize', checkScreenSize)
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.app-header {
  background-color: $white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
  position: relative;
}

.logo{
  
}

.logo img {
  height: 100%;
  padding: 5px;
  max-height: 70px;
  vertical-align: middle;
}

.menu-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;

  .hamburger {
    display: block;
    width: 24px;
    height: 2px;
    background-color: $text-color;
    position: relative;
    transition: background-color 0.3s;

    &::before, &::after {
      content: '';
      position: absolute;
      width: 100%;
      height: 100%;
      background-color: $text-color;
      transition: transform 0.3s;
    }

    &::before { transform: translateY(-8px); }
    &::after { transform: translateY(8px); }
  }
}

nav {
  ul {
    display: flex;
    gap: 2rem;
  }

  a {
    font-weight: 500;
    color: $text-color;
    
    &:hover, &.router-link-active {
      color: $secondary-color;
    }
  }
}

/* Mobile Navigation */
@media (max-width: $bp-md) {
  .menu-toggle {
    display: block;
    z-index: 1001; /* Ensure above nav */
    position: relative;
    
    /* Hamburger Animation */
    .hamburger {
      transition: all 0.3s ease-in-out;
    }
    
    &[aria-expanded="true"] .hamburger {
      background-color: transparent;
      
      &::before {
        transform: rotate(45deg);
        top: 0;
      }
      
      &::after {
        transform: rotate(-45deg);
        top: 0;
      }
    }
  }

  nav {
    position: fixed;
    top: 70px;
    width: 100vw;
    height: 100vh;
    background-color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    left:-100%;
    transition: left 0.4s ease;
    z-index: 1000;

    &.is-open {
      left:0;
    }

    ul {
      flex-direction: column;
      gap: 2rem;
      text-align: center;
      margin-top: -70px;
    }

    a {
      font-size: 1.5rem;
      font-weight: 700;
    }
  }
}
</style>
