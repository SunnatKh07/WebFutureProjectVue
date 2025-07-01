<template>
  <nav class="fixed w-full z-50 transition-all duration-300"
    :class="(scrolled || !isHome) ? 'bg-white/95 backdrop-blur-sm shadow-lg' : 'bg-transparent'">
    <div class="container-custom">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <router-link to="/" class="flex items-center space-x-2 group">
          <div
            class="w-10 h-10 bg-secondary-900 rounded-lg flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
            <span class="text-white font-bold text-xl">W</span>
          </div>
          <span class="font-bold text-xl"
            :class="(scrolled || !isHome) ? 'text-secondary-800' : 'text-white'">WebStudio</span>
        </router-link>

        <!-- Desktop Navigation -->
        <div class="hidden lg:flex items-center space-x-8">
          <router-link v-for="item in navItems" :key="item.name" :to="item.path"
            class="font-medium transition-all duration-300 hover:scale-105 relative group"
            :class="(scrolled || !isHome) ? 'text-secondary-700 hover:text-secondary-900' : 'text-white hover:text-gray-200'">
            {{ item.name }}
            <span
              class="absolute -bottom-1 left-0 w-0 h-0.5 bg-secondary-900 transition-all duration-300 group-hover:w-full"></span>
          </router-link>

          <div class="flex items-center space-x-4 ml-8">
            <router-link to="/login" class="btn-outline text-sm">Вход</router-link>
            <router-link to="/register" class="btn-primary text-sm">Регистрация</router-link>
          </div>
        </div>

        <!-- Mobile menu button -->
        <button @click="toggleMobile" class="lg:hidden p-2 rounded-lg transition-colors duration-300"
          :class="(scrolled || !isHome) ? 'text-secondary-800 hover:bg-secondary-100' : 'text-white hover:bg-white/10'">
          <div class="w-6 h-6 flex flex-col justify-center items-center space-y-1">
            <span class="block w-6 h-0.5 bg-current transition-all duration-300"
              :class="mobileOpen ? 'rotate-45 translate-y-2' : ''"></span>
            <span class="block w-6 h-0.5 bg-current transition-all duration-300"
              :class="mobileOpen ? 'opacity-0' : ''"></span>
            <span class="block w-6 h-0.5 bg-current transition-all duration-300"
              :class="mobileOpen ? '-rotate-45 -translate-y-2' : ''"></span>
          </div>
        </button>
      </div>

      <!-- Mobile Navigation -->
      <transition name="slide-fade">
        <div v-if="mobileOpen" class="lg:hidden bg-white rounded-xl shadow-xl mt-2 overflow-hidden">
          <div class="py-4 space-y-2">
            <router-link v-for="item in navItems" :key="item.name" :to="item.path" @click="mobileOpen = false"
              class="block px-6 py-3 text-secondary-700 hover:bg-gray-50 hover:text-secondary-900 transition-colors duration-300 font-medium">
              {{ item.name }}
            </router-link>
            <div class="border-t border-secondary-100 pt-4 px-6 space-y-2">
              <router-link to="/login" @click="mobileOpen = false" class="block w-full text-center btn-outline text-sm">
                Вход
              </router-link>
              <router-link to="/register" @click="mobileOpen = false"
                class="block w-full text-center btn-primary text-sm">
                Регистрация
              </router-link>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed, watch } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const scrolled = ref(false)
const mobileOpen = ref(false)

const isHome = computed(() => route.path === '/')

const navItems = [
  { name: 'Главная', path: '/' },
  { name: 'О нас', path: '/about' },
  { name: 'Услуги', path: '/services' },
  { name: 'Портфолио', path: '/portfolio' },
  { name: 'Блог', path: '/blog' },
  { name: 'FAQ', path: '/faq' },
  { name: 'Контакты', path: '/contact' }
]

const toggleMobile = () => {
  mobileOpen.value = !mobileOpen.value
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 50
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
  setTimeout(() => {
    handleScroll()
  }, 100)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})

watch(() => route.fullPath, () => {
  scrollToTop()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>
