<template>
  <div class="pt-16 min-h-screen bg-secondary-50 flex items-center justify-center py-12">
    <div class="container-custom">
      <div class="max-w-md mx-auto">
        <div class="card">
          <div class="text-center mb-8">
            <div class="w-16 h-16 bg-gradient-custom rounded-2xl flex items-center justify-center mx-auto mb-4">
              <span class="text-white font-bold text-2xl">W</span>
            </div>
            <h1 class="text-3xl font-bold text-secondary-800 mb-2">Вход в аккаунт</h1>
            <p class="text-secondary-600">Войдите в свой аккаунт для доступа к панели управления</p>
          </div>

          <form @submit.prevent="login" class="space-y-6">
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

            <div>
              <label class="block text-sm font-medium text-secondary-700 mb-2">Пароль</label>
              <div class="relative">
                <input
                  v-model="form.password"
                  :type="showPassword ? 'text' : 'password'"
                  required
                  class="input-field pr-12"
                  :class="{ 'border-red-500': errors.password }"
                  placeholder="Введите пароль"
                >
                <button
                  type="button"
                  @click="showPassword = !showPassword"
                  class="absolute right-3 top-1/2 transform -translate-y-1/2 text-secondary-400 hover:text-secondary-600 transition-colors duration-300"
                >
                  {{ showPassword ? '🙈' : '👁️' }}
                </button>
              </div>
              <p v-if="errors.password" class="text-red-500 text-sm mt-1">{{ errors.password }}</p>
            </div>

            <div class="flex items-center justify-between">
              <div class="flex items-center">
                <input
                  v-model="form.remember"
                  type="checkbox"
                  id="remember"
                  class="w-4 h-4 text-primary-500 border-secondary-300 rounded focus:ring-primary-500"
                >
                <label for="remember" class="ml-2 text-sm text-secondary-600">
                  Запомнить меня
                </label>
              </div>
              <a href="#" class="text-sm text-primary-500 hover:text-primary-600 transition-colors duration-300">
                Забыли пароль?
              </a>
            </div>

            <button
              type="submit"
              :disabled="isSubmitting"
              class="w-full btn-primary"
              :class="{ 'opacity-50 cursor-not-allowed': isSubmitting }"
            >
              {{ isSubmitting ? 'Вход...' : 'Войти' }}
            </button>
          </form>

          <div class="mt-8 text-center">
            <p class="text-secondary-600">
              Нет аккаунта?
              <router-link to="/register" class="text-primary-500 hover:text-primary-600 font-medium transition-colors duration-300">
                Зарегистрироваться
              </router-link>
            </p>
          </div>

          <!-- Social Login -->
          <div class="mt-8">
            <div class="relative">
              <div class="absolute inset-0 flex items-center">
                <div class="w-full border-t border-secondary-200"></div>
              </div>
              <div class="relative flex justify-center text-sm">
                <span class="px-2 bg-white text-secondary-500">или войдите через</span>
              </div>
            </div>

            <div class="mt-6 grid grid-cols-2 gap-4">
              <button
                type="button"
                class="w-full flex items-center justify-center px-4 py-3 border border-secondary-200 rounded-lg hover:bg-secondary-50 transition-colors duration-300"
              >
                <span class="text-xl mr-2">📧</span>
                <span class="text-sm font-medium text-secondary-700">Google</span>
              </button>
              <button
                type="button"
                class="w-full flex items-center justify-center px-4 py-3 border border-secondary-200 rounded-lg hover:bg-secondary-50 transition-colors duration-300"
              >
                <span class="text-xl mr-2">👤</span>
                <span class="text-sm font-medium text-secondary-700">GitHub</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Success Modal -->
    <div
      v-if="showSuccess"
      class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm p-4"
    >
      <div class="bg-white rounded-2xl p-8 max-w-md w-full text-center">
        <div class="w-16 h-16 bg-green-500 rounded-full flex items-center justify-center mx-auto mb-4">
          <span class="text-white text-2xl">✓</span>
        </div>
        <h3 class="text-2xl font-bold text-secondary-800 mb-2">Добро пожаловать!</h3>
        <p class="text-secondary-600 mb-6">
          Вы успешно вошли в систему. Перенаправляем в панель управления...
        </p>
        <div class="w-8 h-8 border-4 border-primary-500 border-t-transparent rounded-full animate-spin mx-auto"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const isSubmitting = ref(false)
const showSuccess = ref(false)
const showPassword = ref(false)

const form = reactive({
  email: '',
  password: '',
  remember: false
})

const errors = reactive({
  email: '',
  password: ''
})

const validateForm = () => {
  errors.email = ''
  errors.password = ''

  let isValid = true

  if (!form.email.trim()) {
    errors.email = 'Email обязателен для заполнения'
    isValid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Введите корректный email'
    isValid = false
  }

  if (!form.password.trim()) {
    errors.password = 'Пароль обязателен для заполнения'
    isValid = false
  } else if (form.password.length < 6) {
    errors.password = 'Пароль должен содержать минимум 6 символов'
    isValid = false
  }

  return isValid
}

const login = async () => {
  if (!validateForm()) return

  isSubmitting.value = true

  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Here you would typically send login data to your API
    console.log('Login attempt:', { email: form.email, password: form.password })
    
    showSuccess.value = true
    
    // Redirect after showing success message
    setTimeout(() => {
      router.push('/')
    }, 2000)
    
  } catch (error) {
    console.error('Login error:', error)
    errors.email = 'Неверный email или пароль'
  } finally {
    isSubmitting.value = false
  }
}
</script>