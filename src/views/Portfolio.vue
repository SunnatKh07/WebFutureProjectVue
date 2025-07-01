<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-purple-50 to-pink-50">
      <div class="container-custom text-center">
        <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
          Наше портфолио
        </h1>
        <p class="text-xl text-secondary-600 max-w-3xl mx-auto leading-relaxed">
          Посмотрите на проекты, которые мы создали с любовью и профессионализмом. 
          Каждая работа - это уникальное решение для конкретного бизнеса.
        </p>
      </div>
    </section>

    <!-- Filter Section -->
    <section class="py-8 bg-white border-b border-secondary-100">
      <div class="container-custom">
        <div class="flex flex-wrap justify-center gap-4">
          <button
            v-for="category in categories"
            :key="category"
            @click="activeCategory = category"
            class="px-6 py-3 rounded-full font-medium transition-all duration-300"
            :class="activeCategory === category 
              ? 'bg-primary-500 text-white shadow-lg' 
              : 'bg-secondary-100 text-secondary-700 hover:bg-secondary-200'"
          >
            {{ category }}
          </button>
        </div>
      </div>
    </section>

    <!-- Portfolio Grid -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="project in filteredProjects"
            :key="project.id"
            class="group cursor-pointer"
            @click="openProject(project)"
          >
            <div class="relative overflow-hidden rounded-2xl shadow-lg group-hover:shadow-2xl transition-all duration-300 transform group-hover:-translate-y-2">
              <div class="h-64 bg-gradient-custom"></div>
              <div class="absolute inset-0 bg-black/20 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center">
                <div class="text-white text-center">
                  <div class="text-2xl mb-2">👁️</div>
                  <span class="font-medium">Посмотреть проект</span>
                </div>
              </div>
              <div class="absolute top-4 right-4">
                <span class="bg-white/90 text-primary-500 text-xs font-semibold px-3 py-1 rounded-full">
                  {{ project.category }}
                </span>
              </div>
            </div>
            <div class="p-6">
              <h3 class="text-xl font-bold text-secondary-800 mb-2 group-hover:text-primary-500 transition-colors duration-300">
                {{ project.title }}
              </h3>
              <p class="text-secondary-600 mb-4">{{ project.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tech in project.technologies"
                  :key="tech"
                  class="bg-secondary-100 text-secondary-700 text-xs px-3 py-1 rounded-full"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Project Modal -->
    <div
      v-if="selectedProject"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4"
      @click="selectedProject = null"
    >
      <div
        class="bg-white rounded-2xl max-w-4xl w-full max-h-[90vh] overflow-y-auto"
        @click.stop
      >
        <div class="relative">
          <div class="h-64 md:h-80 bg-gradient-custom"></div>
          <button
            @click="selectedProject = null"
            class="absolute top-4 right-4 w-10 h-10 bg-white/90 rounded-full flex items-center justify-center hover:bg-white transition-colors duration-300"
          >
            ✕
          </button>
        </div>
        <div class="p-8">
          <div class="flex items-center justify-between mb-6">
            <div>
              <h3 class="text-3xl font-bold text-secondary-800 mb-2">{{ selectedProject.title }}</h3>
              <span class="bg-primary-100 text-primary-700 px-3 py-1 rounded-full text-sm font-medium">
                {{ selectedProject.category }}
              </span>
            </div>
            <div class="text-right">
              <div class="text-sm text-secondary-500 mb-1">Дата завершения</div>
              <div class="font-medium text-secondary-800">{{ selectedProject.date }}</div>
            </div>
          </div>
          
          <div class="space-y-6">
            <div>
              <h4 class="font-semibold text-secondary-800 mb-2">О проекте</h4>
              <p class="text-secondary-600 leading-relaxed">{{ selectedProject.fullDescription }}</p>
            </div>
            
            <div>
              <h4 class="font-semibold text-secondary-800 mb-2">Решенные задачи</h4>
              <ul class="space-y-2">
                <li
                  v-for="task in selectedProject.tasks"
                  :key="task"
                  class="flex items-center space-x-2"
                >
                  <div class="w-4 h-4 bg-primary-500 rounded-full flex items-center justify-center">
                    <span class="text-white text-xs">✓</span>
                  </div>
                  <span class="text-secondary-600">{{ task }}</span>
                </li>
              </ul>
            </div>
            
            <div>
              <h4 class="font-semibold text-secondary-800 mb-3">Технологии</h4>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tech in selectedProject.technologies"
                  :key="tech"
                  class="bg-secondary-100 text-secondary-700 px-3 py-2 rounded-lg font-medium"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
            
            <div class="pt-6 border-t border-secondary-100">
              <div class="flex flex-col sm:flex-row gap-4">
                <button class="btn-primary flex-1">Посетить сайт</button>
                <router-link to="/contact" class="btn-outline flex-1 text-center" @click="selectedProject = null">
                  Заказать похожий
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const activeCategory = ref('Все')
const selectedProject = ref(null)

const categories = ['Все', 'Веб-сайты', 'E-commerce', 'Мобильные', 'Дизайн']

const projects = [
  {
    id: 1,
    title: 'Интернет-магазин ModaStyle',
    description: 'Современный интернет-магазин модной одежды с интуитивным интерфейсом',
    category: 'E-commerce',
    date: 'Декабрь 2023',
    technologies: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe'],
    fullDescription: 'Создали полнофункциональный интернет-магазин модной одежды с современным дизайном и удобной системой управления товарами. Проект включает в себя каталог с фильтрами, корзину покупок, систему оплаты и административную панель.',
    tasks: [
      'Разработка адаптивного дизайна',
      'Интеграция платежной системы',
      'Создание административной панели',
      'Оптимизация для поисковых систем',
      'Настройка аналитики'
    ]
  },
  {
    id: 2,
    title: 'Корпоративный сайт TechCorp',
    description: 'Представительский сайт IT-компании с современным дизайном',
    category: 'Веб-сайты',
    date: 'Ноябрь 2023',
    technologies: ['React', 'Gatsby', 'GraphQL', 'Netlify'],
    fullDescription: 'Разработали корпоративный сайт для IT-компании, который отражает инновационный подход и профессионализм команды. Сайт включает информацию о услугах, портфолио, блог и контактную форму.',
    tasks: [
      'Создание уникального дизайна',
      'Разработка системы блога',
      'Интеграция с CRM системой',
      'Настройка CDN для быстрой загрузки',
      'Внедрение системы аналитики'
    ]
  },
  {
    id: 3,
    title: 'Мобильное приложение FitTracker',
    description: 'Приложение для отслеживания фитнес-активности и здоровья',
    category: 'Мобильные',
    date: 'Октябрь 2023',
    technologies: ['React Native', 'Firebase', 'Redux', 'Chart.js'],
    fullDescription: 'Создали мобильное приложение для отслеживания фитнес-активности с возможностью синхронизации данных, социальными функциями и детальной аналитикой прогресса пользователя.',
    tasks: [
      'Разработка кроссплатформенного приложения',
      'Интеграция с фитнес-трекерами',
      'Создание системы достижений',
      'Реализация социальных функций',
      'Настройка push-уведомлений'
    ]
  },
  {
    id: 4,
    title: 'Ресторан "Вкусная жизнь"',
    description: 'Сайт ресторана с онлайн-бронированием и доставкой',
    category: 'Веб-сайты',
    date: 'Сентябрь 2023',
    technologies: ['WordPress', 'WooCommerce', 'PHP', 'MySQL'],
    fullDescription: 'Разработали сайт для ресторана с возможностью онлайн-бронирования столиков, заказа доставки, просмотра меню и актуальных акций.',
    tasks: [
      'Создание интерактивного меню',
      'Система онлайн-бронирования',
      'Интеграция с доставкой',
      'Мобильная оптимизация',
      'SEO оптимизация'
    ]
  },
  {
    id: 5,
    title: 'Дизайн-система для FinTech',
    description: 'Комплексная дизайн-система для финансового стартапа',
    category: 'Дизайн',
    date: 'Август 2023',
    technologies: ['Figma', 'Sketch', 'Adobe XD', 'Principle'],
    fullDescription: 'Создали полную дизайн-систему для финансового стартапа, включающую компоненты интерфейса, иконки, типографику и руководство по стилю.',
    tasks: [
      'Исследование пользователей',
      'Создание UI Kit',
      'Разработка гайдлайнов',
      'Прототипирование',
      'Тестирование юзабилити'
    ]
  },
  {
    id: 6,
    title: 'Образовательная платформа EduTech',
    description: 'Платформа для онлайн-обучения с интерактивными курсами',
    category: 'Веб-сайты',
    date: 'Июль 2023',
    technologies: ['Vue.js', 'Laravel', 'PostgreSQL', 'Redis'],
    fullDescription: 'Разработали образовательную платформу с системой курсов, тестированием, прогрессом обучения и интерактивными элементами.',
    tasks: [
      'Система управления курсами',
      'Интерактивные тесты и задания',
      'Система оценок и сертификатов',
      'Видеоплеер с функциями',
      'Социальные функции и форум'
    ]
  }
]

const filteredProjects = computed(() => {
  if (activeCategory.value === 'Все') {
    return projects
  }
  return projects.filter(project => project.category === activeCategory.value)
})

const openProject = (project) => {
  selectedProject.value = project
}
</script>