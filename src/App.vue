<template>
  <div class="app-layout" :style="scaleStyle">
    <AppHeader />
    <main>
      <RouterView v-slot="{ Component }">
        <Transition name="fade-up" mode="out-in">
          <component :is="Component" />
        </Transition>
      </RouterView>
    </main>
    <AppFooter />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { RouterView } from 'vue-router'
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'

const windowWidth = ref(window.innerWidth)

const updateWidth = () => {
  windowWidth.value = window.innerWidth
}

const scaleStyle = computed(() => {
  if (windowWidth.value < 320) {
    const scale = windowWidth.value / 320
    return {
      transform: `scale(${scale})`,
      transformOrigin: 'top left',
      width: '320px',
      height: `${100 / scale}vh`,
      overflow: 'hidden'
    }
  }
  return {}
})

onMounted(() => {
  window.addEventListener('resize', updateWidth)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateWidth)
})
</script>

<style scoped>
.app-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1;
}
</style>
