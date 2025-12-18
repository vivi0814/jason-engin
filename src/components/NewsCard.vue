<template>
  <div class="news-card">
    <div class="news-date">{{ date }}</div>
    <h3 class="news-title">{{ title }}</h3>
    <p class="news-summary">{{ summary }}</p>
    <RouterLink :to="`/news/${id}`" class="read-more">閱讀更多 &rarr;</RouterLink>
  </div>
</template>

<script setup>
import { RouterLink } from 'vue-router'

defineProps({
  id: Number,
  date: String,
  title: String,
  summary: String
})
</script>

<style lang="scss" scoped>
@import '../styles/main.scss';

.news-card {
  background: $white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border-left: 4px solid $secondary-color;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  }
}

.news-date {
  font-size: 0.85rem;
  color: #666;
  margin-bottom: 0.5rem;
}

.news-title {
  font-size: 1.25rem;
  color: $primary-color;
  margin-bottom: 0.75rem;
  line-height: 1.4;
}

.news-summary {
  font-size: 0.95rem;
  color: #555;
  margin-bottom: 1rem;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.read-more {
  color: $secondary-color;
  font-weight: 600;
  font-size: 0.9rem;
  
  &:hover {
    text-decoration: underline;
  }
}
</style>
