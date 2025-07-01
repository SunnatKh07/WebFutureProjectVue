<template>
  <footer class="bg-secondary-900 text-white">
    <div class="container-custom section-padding">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        <!-- Company Info -->
        <div class="space-y-4">
          <div class="flex items-center space-x-2">
            <div class="w-10 h-10 bg-gradient-custom rounded-lg flex items-center justify-center">
              <span class="text-white font-bold text-xl">W</span>
            </div>
            <span class="font-bold text-xl">WebStudio</span>
          </div>
          <p class="text-secondary-300 leading-relaxed">
            Создаем современные веб-решения для вашего бизнеса. Профессиональная разработка сайтов и веб-приложений.
          </p>
          <div class="flex space-x-4">
            <a href="#" class="w-10 h-10 bg-secondary-800 rounded-lg flex items-center justify-center hover:bg-primary-500 transition-colors duration-300">
              <span class="text-sm">FB</span>
            </a>
            <a href="#" class="w-10 h-10 bg-secondary-800 rounded-lg flex items-center justify-center hover:bg-primary-500 transition-colors duration-300">
              <span class="text-sm">TW</span>
            </a>
            <a href="#" class="w-10 h-10 bg-secondary-800 rounded-lg flex items-center justify-center hover:bg-primary-500 transition-colors duration-300">
              <span class="text-sm">IG</span>
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div class="space-y-4">
          <h3 class="font-semibold text-lg">Быстрые ссылки</h3>
          <ul class="space-y-2">
            <li v-for="item in quickLinks" :key="item.name">
              <router-link
                :to="item.path"
                class="text-secondary-300 hover:text-white transition-colors duration-300"
              >
                {{ item.name }}
              </router-link>
            </li>
          </ul>
        </div>

        <!-- Services -->
        <div class="space-y-4">
          <h3 class="font-semibold text-lg">Услуги</h3>
          <ul class="space-y-2">
            <li v-for="service in services" :key="service">
              <span class="text-secondary-300">{{ service }}</span>
            </li>
          </ul>
        </div>

        <!-- Contact Info -->
        <div class="space-y-4">
          <h3 class="font-semibold text-lg">Контакты</h3>
          <div class="space-y-3">
            <div class="flex items-center space-x-3">
              <div class="w-5 h-5 text-primary-400">📧</div>
              <span class="text-secondary-300">info@webstudio.com</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="w-5 h-5 text-primary-400">📱</div>
              <span class="text-secondary-300">+7 (555) 123-45-67</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="w-5 h-5 text-primary-400">📍</div>
              <span class="text-secondary-300">Москва, ул. Примерная, 123</span>
            </div>
          </div>
        </div>
      </div>

      <div class="border-t border-secondary-800 mt-12 pt-8 text-center">
        <p class="text-secondary-400">
          © 2024 WebStudio. Все права защищены.
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const quickLinks = [
  { name: 'Главная', path: '/' },
  { name: 'О нас', path: '/about' },
  { name: 'Услуги', path: '/services' },
  { name: 'Портфолио', path: '/portfolio' },
  { name: 'Контакты', path: '/contact' }
]

const services = [
  'Веб-дизайн',
  'Разработка сайтов',
  'Мобильные приложения',
  'SEO оптимизация',
  'Техподдержка'
]
</script>