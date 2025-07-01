<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-orange-50 to-amber-50">
      <div class="container-custom text-center">
        <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
          Наш блог
        </h1>
        <p class="text-xl text-secondary-600 max-w-3xl mx-auto leading-relaxed">
          Полезные статьи о веб-разработке, дизайне, SEO и последних трендах в мире технологий. 
          Делимся опытом и знаниями с нашим сообществом.
        </p>
      </div>
    </section>

    <!-- Filter Section -->
    <section class="py-8 bg-white border-b border-secondary-100">
      <div class="container-custom">
        <div class="flex flex-wrap justify-between items-center gap-4">
          <div class="flex flex-wrap gap-4">
            <button
              v-for="category in categories"
              :key="category"
              @click="activeCategory = category"
              class="px-4 py-2 rounded-full font-medium transition-all duration-300 text-sm"
              :class="activeCategory === category 
                ? 'bg-primary-500 text-white shadow-lg' 
                : 'bg-secondary-100 text-secondary-700 hover:bg-secondary-200'"
            >
              {{ category }}
            </button>
          </div>
          <div class="relative">
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Поиск статей..."
              class="pl-10 pr-4 py-2 border border-secondary-200 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-all duration-300"
            >
            <div class="absolute left-3 top-1/2 transform -translate-y-1/2 text-secondary-400">🔍</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Featured Article -->
    <section class="section-padding bg-secondary-50" v-if="featuredArticle">
      <div class="container-custom">
        <div class="card card-hover cursor-pointer" @click="openArticle(featuredArticle)">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
            <div class="h-64 lg:h-80 bg-gradient-custom rounded-xl"></div>
            <div>
              <span class="bg-primary-100 text-primary-700 px-3 py-1 rounded-full text-sm font-medium mb-4 inline-block">
                Рекомендуемая статья
              </span>
              <h2 class="text-3xl font-bold text-secondary-800 mb-4">{{ featuredArticle.title }}</h2>
              <p class="text-secondary-600 mb-6 leading-relaxed">{{ featuredArticle.excerpt }}</p>
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-4">
                  <div class="w-10 h-10 bg-primary-500 rounded-full flex items-center justify-center">
                    <span class="text-white font-medium text-sm">{{ featuredArticle.author.charAt(0) }}</span>
                  </div>
                  <div>
                    <div class="font-medium text-secondary-800">{{ featuredArticle.author }}</div>
                    <div class="text-sm text-secondary-500">{{ featuredArticle.date }}</div>
                  </div>
                </div>
                <button class="btn-primary">Читать далее</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Articles Grid -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="article in filteredArticles"
            :key="article.id"
            class="card card-hover cursor-pointer group"
            @click="openArticle(article)"
          >
            <div class="h-48 bg-gradient-custom rounded-lg mb-6 relative overflow-hidden">
              <div class="absolute inset-0 bg-black/20 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            </div>
            <div class="space-y-4">
              <div class="flex items-center justify-between">
                <span class="bg-secondary-100 text-secondary-700 px-3 py-1 rounded-full text-xs font-medium">
                  {{ article.category }}
                </span>
                <span class="text-sm text-secondary-500">{{ article.readTime }} мин</span>
              </div>
              <h3 class="text-xl font-bold text-secondary-800 group-hover:text-primary-500 transition-colors duration-300">
                {{ article.title }}
              </h3>
              <p class="text-secondary-600">{{ article.excerpt }}</p>
              <div class="flex items-center justify-between pt-4 border-t border-secondary-100">
                <div class="flex items-center space-x-3">
                  <div class="w-8 h-8 bg-primary-500 rounded-full flex items-center justify-center">
                    <span class="text-white text-xs font-medium">{{ article.author.charAt(0) }}</span>
                  </div>
                  <div>
                    <div class="text-sm font-medium text-secondary-800">{{ article.author }}</div>
                    <div class="text-xs text-secondary-500">{{ article.date }}</div>
                  </div>
                </div>
                <div class="flex items-center space-x-2 text-secondary-400">
                  <span class="text-sm">{{ article.views }}</span>
                  <span>👁️</span>
                </div>
              </div>
            </div>
          </article>
        </div>

        <!-- Load More Button -->
        <div class="text-center mt-12" v-if="hasMoreArticles">
          <button @click="loadMoreArticles" class="btn-outline" :disabled="loadingMore">
            {{ loadingMore ? 'Загрузка...' : 'Загрузить еще' }}
          </button>
        </div>
      </div>
    </section>

    <!-- Article Modal -->
    <div
      v-if="selectedArticle"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4"
      @click="selectedArticle = null"
    >
      <div
        class="bg-white rounded-2xl max-w-4xl w-full max-h-[90vh] overflow-y-auto"
        @click.stop
      >
        <div class="relative">
          <div class="h-64 bg-gradient-custom"></div>
          <button
            @click="selectedArticle = null"
            class="absolute top-4 right-4 w-10 h-10 bg-white/90 rounded-full flex items-center justify-center hover:bg-white transition-colors duration-300"
          >
            ✕
          </button>
        </div>
        <div class="p-8">
          <div class="mb-6">
            <div class="flex items-center justify-between mb-4">
              <span class="bg-primary-100 text-primary-700 px-3 py-1 rounded-full text-sm font-medium">
                {{ selectedArticle.category }}
              </span>
              <span class="text-sm text-secondary-500">{{ selectedArticle.readTime }} мин чтения</span>
            </div>
            <h1 class="text-4xl font-bold text-secondary-800 mb-4">{{ selectedArticle.title }}</h1>
            <div class="flex items-center space-x-4 mb-6">
              <div class="w-12 h-12 bg-primary-500 rounded-full flex items-center justify-center">
                <span class="text-white font-medium">{{ selectedArticle.author.charAt(0) }}</span>
              </div>
              <div>
                <div class="font-medium text-secondary-800">{{ selectedArticle.author }}</div>
                <div class="text-sm text-secondary-500">{{ selectedArticle.date }} • {{ selectedArticle.views }} просмотров</div>
              </div>
            </div>
          </div>
          
          <div class="prose prose-lg max-w-none">
            <p class="text-xl text-secondary-600 leading-relaxed mb-8">{{ selectedArticle.excerpt }}</p>
            <div class="text-secondary-700 leading-relaxed space-y-6">
              <p>{{ selectedArticle.content }}</p>
              <p>В современном мире веб-разработки важно следить за последними трендами и технологиями. Это помогает создавать более эффективные и современные решения для наших клиентов.</p>
              <p>Мы в WebStudio всегда стараемся использовать самые передовые инструменты и методики, что позволяет нам оставаться на переднем крае индустрии и предлагать нашим клиентам решения мирового класса.</p>
            </div>
          </div>
          
          <div class="mt-8 pt-8 border-t border-secondary-100">
            <div class="flex items-center justify-between">
              <div class="flex space-x-4">
                <button class="flex items-center space-x-2 text-secondary-600 hover:text-primary-500 transition-colors duration-300">
                  <span>👍</span>
                  <span>Понравилось</span>
                </button>
                <button class="flex items-center space-x-2 text-secondary-600 hover:text-primary-500 transition-colors duration-300">
                  <span>📤</span>
                  <span>Поделиться</span>
                </button>
              </div>
              <router-link to="/contact" class="btn-primary" @click="selectedArticle = null">
                Обсудить проект
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const searchQuery = ref('')
const activeCategory = ref('Все')
const selectedArticle = ref(null)
const loadingMore = ref(false)
const displayedArticles = ref(6)

const categories = ['Все', 'Разработка', 'Дизайн', 'SEO', 'Тренды', 'Туториалы']

const articles = [
  {
    id: 1,
    title: 'Тренды веб-дизайна 2024: что будет актуально',
    excerpt: 'Разбираем главные тренды в веб-дизайне на 2024 год и как их применить в ваших проектах.',
    content: 'В 2024 году веб-дизайн продолжает эволюционировать, предлагая новые возможности для создания уникальных пользовательских интерфейсов. Минимализм остается актуальным, но теперь он дополняется более смелыми цветовыми решениями и интерактивными элементами.',
    category: 'Дизайн',
    author: 'Мария Сидорова',
    date: '15 декабря 2023',
    readTime: 8,
    views: 1234,
    featured: true
  },
  {
    id: 2,
    title: 'Vue.js 3: полное руководство для начинающих',
    excerpt: 'Изучаем основы Vue.js 3 и создаем первое приложение с использованием Composition API.',
    content: 'Vue.js 3 принес множество улучшений и новых возможностей. Composition API делает код более читаемым и переиспользуемым, а улучшенная производительность позволяет создавать более быстрые приложения.',
    category: 'Разработка',
    author: 'Дмитрий Козлов',
    date: '12 декабря 2023',
    readTime: 12,
    views: 856
  },
  {
    id: 3,
    title: 'SEO в 2024: новые алгоритмы и стратегии',
    excerpt: 'Обновления поисковых алгоритмов и как адаптировать SEO-стратегию под новые требования.',
    content: 'Поисковые системы постоянно совершенствуют свои алгоритмы, делая акцент на качественный контент и пользовательский опыт. Важно понимать эти изменения для эффективного продвижения.',
    category: 'SEO',
    author: 'Ольга Иванова',
    date: '10 декабря 2023',
    readTime: 10,
    views: 642
  },
  {
    id: 4,
    title: 'Создание адаптивного дизайна: лучшие практики',
    excerpt: 'Подробное руководство по созданию дизайна, который отлично выглядит на всех устройствах.',
    content: 'Адаптивный дизайн - это не просто изменение размеров элементов под разные экраны. Это комплексный подход к созданию интерфейсов, которые обеспечивают отличный пользовательский опыт на любом устройстве.',
    category: 'Дизайн',
    author: 'Мария Сидорова',
    date: '8 декабря 2023',
    readTime: 15,
    views: 923
  },
  {
    id: 5,
    title: 'Node.js и Express: создаем API с нуля',
    excerpt: 'Пошаговое создание REST API с использованием Node.js и Express, включая аутентификацию.',
    content: 'Создание надежного API - основа любого современного веб-приложения. Node.js и Express предоставляют все необходимые инструменты для быстрой и эффективной разработки серверной части.',
    category: 'Разработка',
    author: 'Андрей Смирнов',
    date: '5 декабря 2023',
    readTime: 20,
    views: 1456
  },
  {
    id: 6,
    title: 'Микроанимации в веб-интерфейсах: когда и как использовать',
    excerpt: 'Роль микроанимаций в UX и практические советы по их реализации.',
    content: 'Микроанимации способны значительно улучшить пользовательский опыт, делая интерфейс более живым и интуитивным. Главное - использовать их с умом и не перегружать интерфейс.',
    category: 'Дизайн',
    author: 'Мария Сидорова',
    date: '3 декабря 2023',
    readTime: 7,
    views: 734
  },
  {
    id: 7,
    title: 'Безопасность веб-приложений: основные угрозы и защита',
    excerpt: 'Разбираем основные угрозы безопасности и методы защиты веб-приложений.',
    content: 'Безопасность веб-приложений - критически важный аспект разработки. Понимание основных угроз и методов защиты поможет создавать более надежные приложения.',
    category: 'Разработка',
    author: 'Дмитрий Козлов',
    date: '1 декабря 2023',
    readTime: 18,
    views: 892
  },
  {
    id: 8,
    title: 'Цветовая психология в веб-дизайне',
    excerpt: 'Как цвета влияют на восприятие пользователей и принятие решений.',
    content: 'Цвета играют важную роль в восприятии бренда и могут влиять на поведение пользователей. Правильный выбор цветовой палитры может значительно повысить конверсию.',
    category: 'Дизайн',
    author: 'Мария Сидорова',
    date: '28 ноября 2023',
    readTime: 9,
    views: 567
  }
]

const featuredArticle = computed(() => {
  return articles.find(article => article.featured)
})

const filteredArticles = computed(() => {
  let filtered = articles.filter(article => !article.featured)

  if (activeCategory.value !== 'Все') {
    filtered = filtered.filter(article => article.category === activeCategory.value)
  }

  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(article => 
      article.title.toLowerCase().includes(query) || 
      article.excerpt.toLowerCase().includes(query) ||
      article.content.toLowerCase().includes(query)
    )
  }

  return filtered.slice(0, displayedArticles.value)
})

const hasMoreArticles = computed(() => {
  let filtered = articles.filter(article => !article.featured)

  if (activeCategory.value !== 'Все') {
    filtered = filtered.filter(article => article.category === activeCategory.value)
  }

  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(article => 
      article.title.toLowerCase().includes(query) || 
      article.excerpt.toLowerCase().includes(query) ||
      article.content.toLowerCase().includes(query)
    )
  }

  return filtered.length > displayedArticles.value
})

const openArticle = (article) => {
  selectedArticle.value = article
}

const loadMoreArticles = async () => {
  loadingMore.value = true
  
  // Simulate API call
  await new Promise(resolve => setTimeout(resolve, 1000))
  
  displayedArticles.value += 6
  loadingMore.value = false
}

onMounted(() => {
  // Simulate fetching articles from API
  console.log('Articles loaded:', articles.length)
})
</script>