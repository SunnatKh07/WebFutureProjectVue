<template>
  <div class="pt-16">
    <!-- Hero Section -->
    <section class="section-padding bg-gradient-to-br from-cyan-50 to-blue-50">
      <div class="container-custom text-center">
        <h1 class="text-5xl md:text-6xl font-bold text-secondary-800 mb-6">
          Свяжитесь с нами
        </h1>
        <p class="text-xl text-secondary-600 max-w-3xl mx-auto leading-relaxed">
          Готовы обсудить ваш проект? Мы всегда открыты для новых идей и интересных задач. 
          Выберите удобный способ связи или заполните форму ниже.
        </p>
      </div>
    </section>

    <!-- Contact Methods -->
    <section class="section-padding bg-white">
      <div class="container-custom">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-16">
          <div class="text-center group">
            <div class="w-16 h-16 bg-primary-500 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-300">
              <span class="text-white text-2xl">📧</span>
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-2">Email</h3>
            <a href="mailto:info@webstudio.com" class="text-primary-500 hover:text-primary-600 transition-colors duration-300">
              info@webstudio.com
            </a>
          </div>
          
          <div class="text-center group">
            <div class="w-16 h-16 bg-primary-500 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-300">
              <span class="text-white text-2xl">📱</span>
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-2">Телефон</h3>
            <a href="tel:+7555123456" class="text-primary-500 hover:text-primary-600 transition-colors duration-300">
              +7 (555) 123-45-67
            </a>
          </div>
          
          <div class="text-center group">
            <div class="w-16 h-16 bg-primary-500 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-300">
              <span class="text-white text-2xl">📍</span>
            </div>
            <h3 class="text-xl font-semibold text-secondary-800 mb-2">Адрес</h3>
            <p class="text-secondary-600">Москва, ул. Примерная, 123</p>
          </div>
        </div>

        <!-- Contact Form and Info -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
          <!-- Contact Form -->
          <div class="card">
            <h2 class="text-3xl font-bold text-secondary-800 mb-8">Отправить сообщение</h2>
            <form @submit.prevent="submitForm" class="space-y-6">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label class="block text-sm font-medium text-secondary-700 mb-2">Имя</label>
                  <input
                    v-model="form.name"
                    type="text"
                    required
                    class="input-field"
                    :class="{ 'border-red-500': errors.name }"
                    placeholder="Ваше имя"
                  >
                  <p v-if="errors.name" class="text-red-500 text-sm mt-1">{{ errors.name }}</p>
                </div>
                <div>
                  <label class="block text-sm font-medium text-secondary-700 mb-2">Email</label>
                  <input
                    v-model="form.email"
                    type="email"
                    required
                    class="input-field"
                    :class="{ 'border-red-500': errors.email }"
                    placeholder="your@email.com"
                  >
                  <p v-if="errors.email" class="text-red-500 text-sm mt-1">{{ errors.email }}</p>
                </div>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-secondary-700 mb-2">Телефон</label>
                <input
                  v-model="form.phone"
                  type="tel"
                  class="input-field"
                  placeholder="+7 (xxx) xxx-xx-xx"
                >
              </div>
              
              <div>
                <label class="block text-sm font-medium text-secondary-700 mb-2">Тип проекта</label>
                <select v-model="form.projectType" class="input-field">
                  <option value="">Выберите тип проекта</option>
                  <option value="website">Веб-сайт</option>
                  <option value="ecommerce">Интернет-магазин</option>
                  <option value="mobile">Мобильное приложение</option>
                  <option value="design">Дизайн</option>
                  <option value="seo">SEO продвижение</option>
                  <option value="support">Техподдержка</option>
                  <option value="other">Другое</option>
                </select>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-secondary-700 mb-2">Сообщение</label>
                <textarea
                  v-model="form.message"
                  rows="5"
                  required
                  class="input-field resize-none"
                  :class="{ 'border-red-500': errors.message }"
                  placeholder="Расскажите подробнее о вашем проекте..."
                ></textarea>
                <p v-if="errors.message" class="text-red-500 text-sm mt-1">{{ errors.message }}</p>
              </div>
              
              <div class="flex items-center space-x-3">
                <input
                  v-model="form.agreement"
                  type="checkbox"
                  id="agreement"
                  required
                  class="w-4 h-4 text-primary-500 border-secondary-300 rounded focus:ring-primary-500"
                >
                <label for="agreement" class="text-sm text-secondary-600">
                  Согласен с <a href="#" class="text-primary-500 hover:text-primary-600">политикой конфиденциальности</a>
                </label>
              </div>
              
              <button
                type="submit"
                :disabled="isSubmitting"
                class="w-full btn-primary"
                :class="{ 'opacity-50 cursor-not-allowed': isSubmitting }"
              >
                {{ isSubmitting ? 'Отправка...' : 'Отправить сообщение' }}
              </button>
            </form>
          </div>

          <!-- Additional Info -->
          <div class="space-y-8">
            <div class="card">
              <h3 class="text-2xl font-bold text-secondary-800 mb-4">Время работы</h3>
              <div class="space-y-3">
                <div class="flex justify-between">
                  <span class="text-secondary-600">Пн - Пт:</span>
                  <span class="font-medium text-secondary-800">9:00 - 18:00</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-secondary-600">Сб:</span>
                  <span class="font-medium text-secondary-800">10:00 - 16:00</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-secondary-600">Вс:</span>
                  <span class="font-medium text-secondary-800">Выходной</span>
                </div>
              </div>
            </div>

            <div class="card">
              <h3 class="text-2xl font-bold text-secondary-800 mb-4">Социальные сети</h3>
              <div class="flex space-x-4">
                <a href="#" class="w-12 h-12 bg-primary-500 rounded-lg flex items-center justify-center text-white hover:bg-primary-600 transition-colors duration-300">
                  FB
                </a>
                <a href="#" class="w-12 h-12 bg-primary-500 rounded-lg flex items-center justify-center text-white hover:bg-primary-600 transition-colors duration-300">
                  TW
                </a>
                <a href="#" class="w-12 h-12 bg-primary-500 rounded-lg flex items-center justify-center text-white hover:bg-primary-600 transition-colors duration-300">
                  IG
                </a>
                <a href="#" class="w-12 h-12 bg-primary-500 rounded-lg flex items-center justify-center text-white hover:bg-primary-600 transition-colors duration-300">
                  LI
                </a>
              </div>
            </div>

            <div class="card">
              <h3 class="text-2xl font-bold text-secondary-800 mb-4">Быстрая связь</h3>
              <p class="text-secondary-600 mb-4">
                Нужна срочная консультация? Звоните прямо сейчас!
              </p>
              <a href="tel:+7555123456" class="btn-primary text-center block">
                Позвонить сейчас
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Success Modal -->
    <div
      v-if="showSuccess"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm p-4"
      @click="showSuccess = false"
    >
      <div class="bg-white rounded-2xl p-8 max-w-md w-full text-center" @click.stop>
        <div class="w-16 h-16 bg-green-500 rounded-full flex items-center justify-center mx-auto mb-4">
          <span class="text-white text-2xl">✓</span>
        </div>
        <h3 class="text-2xl font-bold text-secondary-800 mb-2">Сообщение отправлено!</h3>
        <p class="text-secondary-600 mb-6">
          Спасибо за ваше обращение. Мы свяжемся с вами в ближайшее время.
        </p>
        <button @click="showSuccess = false" class="btn-primary">
          Закрыть
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import axios from 'axios'

const isSubmitting = ref(false)
const showSuccess = ref(false)

const form = reactive({
  name: '',
  email: '',
  phone: '',
  projectType: '',
  message: '',
  agreement: false
})

const errors = reactive({
  name: '',
  email: '',
  message: ''
})

const validateForm = () => {
  errors.name = ''
  errors.email = ''
  errors.message = ''

  let isValid = true

  if (!form.name.trim()) {
    errors.name = 'Имя обязательно для заполнения'
    isValid = false
  }

  if (!form.email.trim()) {
    errors.email = 'Email обязателен для заполнения'
    isValid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Введите корректный email'
    isValid = false
  }

  if (!form.message.trim()) {
    errors.message = 'Сообщение обязательно для заполнения'
    isValid = false
  }

  return isValid
}

const submitForm = async () => {
  if (!validateForm()) return

  isSubmitting.value = true

  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Here you would typically send the form data to your API
    // await axios.post('/api/contact', form)
    
    console.log('Form submitted:', form)
    
    // Reset form
    Object.keys(form).forEach(key => {
      if (typeof form[key] === 'boolean') {
        form[key] = false
      } else {
        form[key] = ''
      }
    })
    
    showSuccess.value = true
  } catch (error) {
    console.error('Error submitting form:', error)
    alert('Произошла ошибка при отправке формы. Пожалуйста, попробуйте еще раз.')
  } finally {
    isSubmitting.value = false
  }
}
</script>