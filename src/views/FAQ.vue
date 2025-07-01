<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-green-50 to-teal-50">
      <div class="container-custom text-center">
        <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
          Часто задаваемые вопросы
        </h1>
        <p class="text-xl text-secondary-600 max-w-3xl mx-auto leading-relaxed">
          Ответы на самые популярные вопросы о наших услугах, процессе работы и условиях сотрудничества.
        </p>
      </div>
    </section>

    <!-- Search Section -->
    <section class="py-8 bg-white border-b border-secondary-100">
      <div class="container-custom">
        <div class="max-w-2xl mx-auto">
          <div class="relative">
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Найти ответ на вопрос..."
              class="w-full pl-12 pr-4 py-4 border border-secondary-200 rounded-xl focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-all duration-300 text-lg"
            >
            <div class="absolute left-4 top-1/2 transform -translate-y-1/2 text-2xl">🔍</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Categories -->
    <section class="py-8 bg-secondary-50">
      <div class="container-custom">
        <div class="flex flex-wrap justify-center gap-4">
          <button
            v-for="category in categories"
            :key="category"
            @click="activeCategory = category"
            class="px-6 py-3 rounded-full font-medium transition-all duration-300"
            :class="activeCategory === category 
              ? 'bg-primary-500 text-white shadow-lg' 
              : 'bg-white text-secondary-700 hover:bg-secondary-100 shadow-sm'"
          >
            {{ category }}
          </button>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <div class="space-y-4">
            <div
              v-for="(faq, index) in filteredFAQ"
              :key="index"
              class="border border-secondary-200 rounded-xl overflow-hidden hover:shadow-lg transition-all duration-300"
            >
              <button
                @click="toggleFAQ(index)"
                class="w-full p-6 text-left flex items-center justify-between hover:bg-secondary-50 transition-colors duration-300"
              >
                <h3 class="text-lg font-semibold text-secondary-800 pr-4">{{ faq.question }}</h3>
                <div class="text-2xl text-primary-500 transform transition-transform duration-300"
                     :class="openFAQ === index ? 'rotate-45' : ''">
                  +
                </div>
              </button>
              <transition name="slide-fade">
                <div v-if="openFAQ === index" class="px-6 pb-6">
                  <div class="text-secondary-600 leading-relaxed">
                    {{ faq.answer }}
                  </div>
                  <div v-if="faq.additionalInfo" class="mt-4 p-4 bg-primary-50 rounded-lg">
                    <div class="text-sm text-primary-700">
                      <strong>Дополнительно:</strong> {{ faq.additionalInfo }}
                    </div>
                  </div>
                </div>
              </transition>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact CTA -->
    <section class="section-padding bg-secondary-900 text-white">
      <div class="container-custom text-center">
        <h2 class="text-3xl md:text-4xl font-bold mb-4">
          Не нашли ответ на свой вопрос?
        </h2>
        <p class="text-xl mb-8 text-secondary-300 max-w-2xl mx-auto">
          Наша команда всегда готова помочь. Свяжитесь с нами любым удобным способом.
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <router-link to="/contact" class="btn-primary">
            Задать вопрос
          </router-link>
          <a href="tel:+7555123456" class="btn-outline border-white text-white hover:bg-white hover:text-secondary-800">
            Позвонить сейчас
          </a>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const searchQuery = ref('')
const activeCategory = ref('Все')
const openFAQ = ref(null)

const categories = ['Все', 'Общие', 'Разработка', 'Дизайн', 'Оплата', 'Поддержка']

const faqs = [
  {
    category: 'Общие',
    question: 'Сколько времени занимает разработка сайта?',
    answer: 'Время разработки зависит от сложности проекта. Простой сайт-визитка занимает 1-2 недели, корпоративный сайт - 3-4 недели, а интернет-магазин может потребовать 6-8 недель.',
    additionalInfo: 'Мы всегда стараемся уложиться в оговоренные сроки и информируем о ходе работ еженедельно.'
  },
  {
    category: 'Общие',
    question: 'Предоставляете ли вы техническую поддержку?',
    answer: 'Да, мы предоставляем техническую поддержку для всех наших проектов. Первые 3 месяца поддержка бесплатная, далее на основе договора обслуживания.',
    additionalInfo: 'Поддержка включает устранение ошибок, обновления контента и консультации.'
  },
  {
    category: 'Разработка',
    question: 'Какие технологии вы используете?',
    answer: 'Мы работаем с современными технологиями: Vue.js, React, Node.js, PHP, Python, WordPress, Shopify и многими другими. Выбор технологий зависит от требований проекта.',
    additionalInfo: 'Мы постоянно изучаем новые технологии, чтобы предлагать самые эффективные решения.'
  },
  {
    category: 'Разработка',
    question: 'Адаптируете ли сайты под мобильные устройства?',
    answer: 'Абсолютно все наши сайты адаптивны и корректно отображаются на мобильных устройствах, планшетах и десктопах. Это стандарт нашей работы.',
    additionalInfo: 'Мы тестируем сайты на различных устройствах и браузерах перед запуском.'
  },
  {
    category: 'Дизайн',
    question: 'Создаете ли вы уникальный дизайн?',
    answer: 'Да, мы создаем индивидуальный дизайн для каждого проекта. Не используем готовые шаблоны - каждый дизайн разрабатывается с учетом специфики вашего бизнеса.',
    additionalInfo: 'Процесс включает исследование, создание концепции, прототипирование и финальный дизайн.'
  },
  {
    category: 'Дизайн',
    question: 'Сколько вариантов дизайна вы предлагаете?',
    answer: 'Обычно мы предлагаем 2-3 концепции дизайна на выбор. После выбора концепции дорабатываем дизайн до полного соответствия вашим требованиям.',
    additionalInfo: 'Количество правок не ограничено до момента утверждения финального дизайна.'
  },
  {
    category: 'Оплата',
    question: 'Какие способы оплаты вы принимаете?',
    answer: 'Мы принимаем оплату банковскими переводами, картами, через PayPal и другие электронные платежные системы. Работаем как с физическими, так и с юридическими лицами.',
    additionalInfo: 'Предоставляем все необходимые документы для отчетности вашей бухгалтерии.'
  },
  {
    category: 'Оплата',
    question: 'Возможна ли оплата в рассрочку?',
    answer: 'Да, для крупных проектов мы предлагаем поэтапную оплату. Обычно это 50% предоплата, 30% после согласования дизайна и 20% после завершения проекта.',
    additionalInfo: 'Схема оплаты обсуждается индивидуально для каждого проекта.'
  },
  {
    category: 'Поддержка',
    question: 'Обучаете ли вы работе с сайтом?',
    answer: 'Да, мы проводим обучение для ваших сотрудников по работе с административной панелью сайта. Также предоставляем подробную документацию.',
    additionalInfo: 'Обучение может проводиться очно, онлайн или в записи - как вам удобнее.'
  },
  {
    category: 'Поддержка',
    question: 'Что делать, если сайт сломался?',
    answer: 'Если возникли проблемы с сайтом, немедленно свяжитесь с нами. В рамках гарантийного обслуживания мы бесплатно устраним все неполадки в кратчайшие сроки.',
    additionalInfo: 'Среднее время реакции на критические проблемы - 2 часа в рабочее время.'
  }
]

const filteredFAQ = computed(() => {
  let filtered = faqs

  if (activeCategory.value !== 'Все') {
    filtered = filtered.filter(faq => faq.category === activeCategory.value)
  }

  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(faq => 
      faq.question.toLowerCase().includes(query) || 
      faq.answer.toLowerCase().includes(query)
    )
  }

  return filtered
})

const toggleFAQ = (index) => {
  openFAQ.value = openFAQ.value === index ? null : index
}
</script>