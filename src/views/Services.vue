<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-blue-50 to-indigo-50">
      <div class="container-custom text-center">
        <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
          Наши услуги
        </h1>
        <p class="text-xl text-secondary-600 max-w-3xl mx-auto leading-relaxed">
          Полный спектр решений для вашего цифрового присутствия. 
          От идеи до реализации - мы воплощаем ваши мечты в реальность.
        </p>
      </div>
    </section>

    <!-- Services Grid -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="card card-hover group cursor-pointer"
            @click="selectService(service)"
          >
            <div class="text-5xl mb-6 group-hover:scale-110 transition-transform duration-300">
              {{ service.icon }}
            </div>
            <h3 class="text-2xl font-bold text-secondary-800 mb-4">{{ service.title }}</h3>
            <p class="text-secondary-600 mb-6 leading-relaxed">{{ service.description }}</p>
            <div class="space-y-2 mb-6">
              <div
                v-for="feature in service.features"
                :key="feature"
                class="flex items-center space-x-2"
              >
                <div class="w-4 h-4 bg-primary-500 rounded-full flex items-center justify-center">
                  <span class="text-white text-xs">✓</span>
                </div>
                <span class="text-sm text-secondary-600">{{ feature }}</span>
              </div>
            </div>
            <div class="flex items-center justify-between">
              <span class="text-2xl font-bold text-primary-500">от {{ service.price }}</span>
              <button class="btn-primary text-sm">Подробнее</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Process Section -->
    <section class="section-padding bg-secondary-50">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-secondary-800 mb-4">
            Процесс работы
          </h2>
          <p class="text-xl text-secondary-600 max-w-2xl mx-auto">
            Прозрачный и эффективный подход к реализации ваших проектов
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(step, index) in process"
            :key="index"
            class="text-center group"
          >
            <div class="relative mb-6">
              <div class="w-16 h-16 bg-primary-500 rounded-full flex items-center justify-center mx-auto group-hover:scale-110 transition-transform duration-300">
                <span class="text-white font-bold text-xl">{{ index + 1 }}</span>
              </div>
              <div v-if="index < process.length - 1" class="hidden lg:block absolute top-8 left-full w-full h-0.5 bg-primary-200 -translate-x-8"></div>
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-3">{{ step.title }}</h3>
            <p class="text-secondary-600">{{ step.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Technology Section -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-secondary-800 mb-4">
            Технологии
          </h2>
          <p class="text-xl text-secondary-600">
            Используем самые современные инструменты и технологии
          </p>
        </div>

        <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-8">
          <div
            v-for="(tech, index) in technologies"
            :key="index"
            class="text-center group"
          >
            <div class="w-16 h-16 bg-secondary-100 rounded-xl flex items-center justify-center mx-auto mb-3 group-hover:bg-primary-500 group-hover:scale-110 transition-all duration-300">
              <span class="text-2xl group-hover:text-white">{{ tech.icon }}</span>
            </div>
            <span class="text-sm font-medium text-secondary-700 group-hover:text-primary-500 transition-colors duration-300">
              {{ tech.name }}
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- Service Modal -->
    <div
      v-if="selectedService"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm p-4"
      @click="selectedService = null"
    >
      <div
        class="bg-white rounded-2xl max-w-2xl w-full max-h-[80vh] overflow-y-auto"
        @click.stop
      >
        <div class="p-8">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-3xl font-bold text-secondary-800">{{ selectedService.title }}</h3>
            <button
              @click="selectedService = null"
              class="w-8 h-8 bg-secondary-100 rounded-full flex items-center justify-center hover:bg-secondary-200 transition-colors duration-300"
            >
              ✕
            </button>
          </div>
          <div class="space-y-6">
            <p class="text-secondary-600 leading-relaxed">{{ selectedService.fullDescription }}</p>
            <div>
              <h4 class="font-semibold text-secondary-800 mb-3">Что включено:</h4>
              <ul class="space-y-2">
                <li
                  v-for="feature in selectedService.fullFeatures"
                  :key="feature"
                  class="flex items-center space-x-2"
                >
                  <div class="w-4 h-4 bg-primary-500 rounded-full flex items-center justify-center">
                    <span class="text-white text-xs">✓</span>
                  </div>
                  <span class="text-secondary-600">{{ feature }}</span>
                </li>
              </ul>
            </div>
            <div class="flex items-center justify-between pt-6 border-t border-secondary-100">
              <span class="text-3xl font-bold text-primary-500">от {{ selectedService.price }}</span>
              <router-link to="/contact" class="btn-primary" @click="selectedService = null">
                Заказать услугу
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const selectedService = ref(null)

const selectService = (service) => {
  selectedService.value = service
}

const services = [
  {
    icon: '🌐',
    title: 'Веб-разработка',
    description: 'Создание современных веб-сайтов и приложений с использованием передовых технологий.',
    features: ['Адаптивный дизайн', 'SEO оптимизация', 'Быстрая загрузка'],
    price: '50 000₽',
    fullDescription: 'Полный цикл веб-разработки от концепции до запуска. Мы создаем сайты, которые не только красиво выглядят, но и эффективно работают на всех устройствах.',
    fullFeatures: ['Адаптивный дизайн для всех устройств', 'SEO оптимизация', 'Быстрая загрузка страниц', 'Интеграция с CMS', 'Техническая поддержка', 'Обучение администрированию']
  },
  {
    icon: '📱',
    title: 'Мобильные приложения',
    description: 'Разработка нативных и кроссплатформенных мобильных приложений.',
    features: ['iOS & Android', 'Современный UI/UX', 'Push-уведомления'],
    price: '80 000₽',
    fullDescription: 'Создаем мобильные приложения, которые обеспечивают отличный пользовательский опыт и помогают вашему бизнесу расти.',
    fullFeatures: ['Нативная разработка для iOS и Android', 'Современный UI/UX дизайн', 'Push-уведомления', 'Интеграция с API', 'Публикация в App Store и Google Play', 'Аналитика и метрики']
  },
  {
    icon: '🎨',
    title: 'UI/UX Дизайн',
    description: 'Создание интуитивно понятных и визуально привлекательных интерфейсов.',
    features: ['Пользовательское исследование', 'Прототипирование', 'Дизайн-система'],
    price: '30 000₽',
    fullDescription: 'Проектируем пользовательские интерфейсы, которые не только красиво выглядят, но и обеспечивают отличный пользовательский опыт.',
    fullFeatures: ['Пользовательское исследование', 'Создание wireframes и прототипов', 'Визуальный дизайн', 'Дизайн-система', 'Интерактивные прототипы', 'Передача в разработку']
  },
  {
    icon: '🛒',
    title: 'E-commerce',
    description: 'Интернет-магазины с полным функционалом для онлайн-продаж.',
    features: ['Каталог товаров', 'Система оплат', 'Управление заказами'],
    price: '100 000₽',
    fullDescription: 'Создаем полнофункциональные интернет-магазины, которые помогают увеличить продажи и улучшить взаимодействие с клиентами.',
    fullFeatures: ['Каталог товаров с фильтрами', 'Корзина и оформление заказов', 'Система оплат', 'Управление заказами', 'Интеграция с CRM', 'Аналитика продаж']
  },
  {
    icon: '🔧',
    title: 'Техподдержка',
    description: 'Комплексная техническая поддержка и сопровождение ваших проектов.',
    features: ['24/7 мониторинг', 'Обновления', 'Резервное копирование'],
    price: '15 000₽/мес',
    fullDescription: 'Обеспечиваем стабильную работу ваших веб-ресурсов с круглосуточным мониторингом и оперативным устранением проблем.',
    fullFeatures: ['24/7 мониторинг работы сайта', 'Регулярные обновления', 'Резервное копирование', 'Устранение ошибок', 'Оптимизация производительности', 'Консультации по развитию']
  },
  {
    icon: '📈',
    title: 'SEO продвижение',
    description: 'Комплексная поисковая оптимизация для увеличения органического трафика.',
    features: ['Анализ конкурентов', 'Техническая оптимизация', 'Контент-стратегия'],
    price: '25 000₽/мес',
    fullDescription: 'Помогаем вашему сайту подняться в топ поисковых результатов и привлечь больше целевых посетителей.',
    fullFeatures: ['Анализ конкурентов и ключевых слов', 'Техническая оптимизация сайта', 'Контент-стратегия', 'Линкбилдинг', 'Отчеты о результатах', 'Постоянная оптимизация']
  }
]

const process = [
  {
    title: 'Консультация',
    description: 'Обсуждаем ваши цели и требования к проекту'
  },
  {
    title: 'Планирование',
    description: 'Создаем детальный план реализации проекта'
  },
  {
    title: 'Разработка',
    description: 'Воплощаем идеи в жизнь с регулярными отчетами'
  },
  {
    title: 'Запуск',
    description: 'Тестируем, запускаем и передаем готовый проект'
  }
]

const technologies = [
  { name: 'Vue.js', icon: '⚡' },
  { name: 'React', icon: '⚛️' },
  { name: 'Node.js', icon: '🟢' },
  { name: 'PHP', icon: '🐘' },
  { name: 'Python', icon: '🐍' },
  { name: 'WordPress', icon: '📝' },
  { name: 'Shopify', icon: '🛍️' },
  { name: 'Figma', icon: '🎨' },
  { name: 'Docker', icon: '🐋' },
  { name: 'AWS', icon: '☁️' },
  { name: 'Git', icon: '📋' },
  { name: 'MySQL', icon: '🗄️' }
]
</script>