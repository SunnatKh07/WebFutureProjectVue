<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-primary-50 to-purple-50">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto text-center">
          <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
            О нашей компании
          </h1>
          <p class="text-xl text-secondary-600 leading-relaxed">
            Мы команда профессионалов, которая создает выдающиеся веб-решения уже более 5 лет. 
            Наша страсть к инновациям и качеству помогает бизнесу достигать новых высот в цифровом мире.
          </p>
        </div>
      </div>
    </section>

    <!-- Mission Section -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div>
            <h2 class="text-4xl font-bold text-secondary-800 mb-6">
              Наша миссия
            </h2>
            <p class="text-lg text-secondary-600 mb-6 leading-relaxed">
              Мы стремимся создавать веб-решения, которые не просто работают, а вдохновляют. 
              Каждый проект для нас - это возможность воплотить инновационные идеи и помочь 
              нашим клиентам достичь успеха в цифровой среде.
            </p>
            <div class="space-y-4">
              <div class="flex items-center space-x-3">
                <div class="w-6 h-6 bg-primary-500 rounded-full flex items-center justify-center">
                  <span class="text-white text-sm">✓</span>
                </div>
                <span class="text-secondary-700">Индивидуальный подход к каждому проекту</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-6 h-6 bg-primary-500 rounded-full flex items-center justify-center">
                  <span class="text-white text-sm">✓</span>
                </div>
                <span class="text-secondary-700">Использование передовых технологий</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-6 h-6 bg-primary-500 rounded-full flex items-center justify-center">
                  <span class="text-white text-sm">✓</span>
                </div>
                <span class="text-secondary-700">Постоянная поддержка и развитие</span>
              </div>
            </div>
          </div>
          <div class="relative">
            <div class="w-full h-96 bg-gradient-custom rounded-2xl shadow-2xl"></div>
            <div class="absolute inset-4 bg-white/10 rounded-xl backdrop-blur-sm"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section class="section-padding bg-secondary-50">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-secondary-800 mb-4">
            Наша команда
          </h2>
          <p class="text-xl text-secondary-600 max-w-2xl mx-auto">
            Профессионалы своего дела, которые воплощают самые смелые идеи в реальность
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(member, index) in team"
            :key="index"
            class="card card-hover text-center group"
          >
            <div class="w-24 h-24 bg-gradient-custom rounded-full mx-auto mb-4 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
              <span class="text-white text-2xl font-bold">{{ member.name.charAt(0) }}</span>
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-2">{{ member.name }}</h3>
            <p class="text-primary-500 font-medium mb-3">{{ member.position }}</p>
            <p class="text-secondary-600 text-sm leading-relaxed">{{ member.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Values Section -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-bold text-secondary-800 mb-4">
            Наши ценности
          </h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(value, index) in values"
            :key="index"
            class="text-center group"
          >
            <div class="text-5xl mb-4 group-hover:scale-110 transition-transform duration-300">
              {{ value.icon }}
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-3">{{ value.title }}</h3>
            <p class="text-secondary-600">{{ value.description }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const team = [
  {
    name: 'Алексей Петров',
    position: 'CEO & Основатель',
    description: 'Опытный руководитель с 10-летним стажем в IT-индустрии. Ведет компанию к новым достижениям.'
  },
  {
    name: 'Мария Сидорова',
    position: 'Главный дизайнер',
    description: 'Творческий визионер, создающий уникальные и функциональные дизайны для наших клиентов.'
  },
  {
    name: 'Дмитрий Козлов',
    position: 'Lead Developer',
    description: 'Технический эксперт с глубокими знаниями современных веб-технологий и архитектуры.'
  },
  {
    name: 'Елена Волкова',
    position: 'Project Manager',
    description: 'Организует работу команды и обеспечивает своевременную реализацию проектов.'
  },
  {
    name: 'Андрей Смирнов',
    position: 'Frontend Developer',
    description: 'Специалист по созданию интерактивных пользовательских интерфейсов.'
  },
  {
    name: 'Ольга Иванова',
    position: 'SEO Specialist',
    description: 'Эксперт по поисковой оптимизации и цифровому маркетингу.'
  }
]

const values = [
  {
    icon: '💡',
    title: 'Инновации',
    description: 'Всегда идем в ногу с последними технологиями'
  },
  {
    icon: '🤝',
    title: 'Партнерство',
    description: 'Строим долгосрочные отношения с клиентами'
  },
  {
    icon: '⭐',
    title: 'Качество',
    description: 'Никогда не идем на компромиссы в вопросах качества'
  },
  {
    icon: '🎯',
    title: 'Результат',
    description: 'Фокусируемся на достижении поставленных целей'
  }
]
</script>