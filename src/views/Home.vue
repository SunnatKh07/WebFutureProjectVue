<template>
  <div>
    <!-- Hero Section -->
    <section class="relative min-h-screen flex items-center justify-center bg-gradient-custom overflow-hidden">
      <div class="absolute inset-0 bg-black/30"></div>
      
      <!-- Animated background elements -->
      <div class="absolute inset-0">
        <div class="absolute top-20 left-10 w-32 h-32 bg-white/5 rounded-full animate-bounce-gentle"></div>
        <div class="absolute bottom-20 right-10 w-24 h-24 bg-white/5 rounded-full animate-bounce-gentle" style="animation-delay: 1s"></div>
        <div class="absolute top-1/2 left-1/4 w-16 h-16 bg-white/5 rounded-full animate-bounce-gentle" style="animation-delay: 2s"></div>
      </div>

      <div class="container-custom relative z-10 text-center text-white">
        <h1 class="text-5xl md:text-7xl font-bold mb-6 animate-fade-in">
          Создаем будущее
          <span class="block text-transparent bg-clip-text bg-gradient-to-r from-gray-200 to-white">
            веб-технологий
          </span>
        </h1>
        <p class="text-xl md:text-2xl mb-8 max-w-3xl mx-auto leading-relaxed opacity-90 animate-slide-up">
          Профессиональная разработка сайтов и веб-приложений. Превращаем ваши идеи в цифровые решения мирового класса.
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center animate-slide-up" style="animation-delay: 0.3s">
          <router-link to="/portfolio" class="btn-primary text-lg px-8 py-4 bg-white text-secondary-900 hover:bg-gray-100">
            Посмотреть работы
          </router-link>
          <router-link to="/contact" class="btn-outline text-lg px-8 py-4 border-white text-white hover:bg-white hover:text-secondary-800">
            Связаться с нами
          </router-link>
        </div>
      </div>

      <!-- Scroll indicator -->
      <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 animate-bounce">
        <div class="w-6 h-10 border-2 border-white rounded-full flex justify-center">
          <div class="w-1 h-3 bg-white rounded-full mt-2 animate-pulse"></div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="section-padding bg-gray-50">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-secondary-800 mb-4">
            Почему выбирают нас
          </h2>
          <p class="text-xl text-secondary-600 max-w-2xl mx-auto">
            Мы предлагаем полный спектр услуг для создания вашего идеального веб-присутствия
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(feature, index) in features"
            :key="index"
            class="card card-hover group cursor-pointer"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div class="text-4xl mb-4 group-hover:scale-110 transition-transform duration-300">
              {{ feature.icon }}
            </div>
            <h3 class="text-xl font-semibold mb-3 text-secondary-800">{{ feature.title }}</h3>
            <p class="text-secondary-600 leading-relaxed">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="text-center group"
          >
            <div class="text-4xl md:text-5xl font-bold text-secondary-800 mb-2 group-hover:scale-110 transition-transform duration-300">
              {{ stat.number }}
            </div>
            <div class="text-secondary-600 font-medium">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="section-padding bg-secondary-900 text-white">
      <div class="container-custom text-center">
        <h2 class="text-4xl md:text-5xl font-bold mb-6">
          Готовы начать проект?
        </h2>
        <p class="text-xl mb-8 max-w-2xl mx-auto text-gray-300">
          Свяжитесь с нами сегодня и получите бесплатную консультацию по вашему проекту
        </p>
        <router-link to="/contact" class="btn-primary text-lg px-8 py-4 inline-block bg-white text-secondary-900 hover:bg-gray-100">
          Получить консультацию
        </router-link>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const features = [
  {
    icon: '🚀',
    title: 'Современные технологии',
    description: 'Используем последние веб-технологии для создания быстрых и надежных решений'
  },
  {
    icon: '🎨',
    title: 'Уникальный дизайн',
    description: 'Создаем индивидуальный дизайн, который отражает специфику вашего бизнеса'
  },
  {
    icon: '📱',
    title: 'Адаптивность',
    description: 'Все наши проекты корректно отображаются на любых устройствах'
  },
  {
    icon: '⚡',
    title: 'Высокая скорость',
    description: 'Оптимизируем каждый элемент для максимальной производительности'
  },
  {
    icon: '🔒',
    title: 'Безопасность',
    description: 'Применяем современные методы защиты для обеспечения безопасности данных'
  },
  {
    icon: '🎯',
    title: 'SEO оптимизация',
    description: 'Настраиваем сайт для высоких позиций в поисковых системах'
  }
]

const stats = [
  { number: '200+', label: 'Проектов' },
  { number: '150+', label: 'Клиентов' },
  { number: '5', label: 'Лет опыта' },
  { number: '24/7', label: 'Поддержка' }
]
</script>