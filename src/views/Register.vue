<template>
  <div class="pt-16 min-h-screen bg-secondary-50 flex items-center justify-center py-12">
    <div class="container-custom">
      <div class="max-w-md mx-auto">
        <div class="card">
          <div class="text-center mb-8">
            <div class="w-16 h-16 bg-gradient-custom rounded-2xl flex items-center justify-center mx-auto mb-4">
              <span class="text-white font-bold text-2xl">W</span>
            </div>
            <h1 class="text-3xl font-bold text-secondary-800 mb-2">Регистрация</h1>
            <p class="text-secondary-600">Создайте аккаунт для доступа к нашим услугам</p>
          </div>

          <form @submit.prevent="register" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label class="block text-sm font-medium text-secondary-700 mb-2">Имя</label>
                <input
                  v-model="form.firstName"
                  type="text"
                  required
                  class="input-field"
                  :class="{ 'border-red-500': errors.firstName }"
                  placeholder="Ваше имя"
                >
                <p v-if="errors.firstName" class="text-red-500 text-sm mt-1">{{ errors.firstName }}</p>
              </div>
              <div>
                <label class="block text-sm font-medium text-secondary-700 mb-2">Фамилия</label>
                <input
                  v-model="form.lastName"
                  type="text"
                  required
                  class="input-field"
                  :class="{ 'border-red-500': errors.lastName }"
                  placeholder="Ваша фамилия"
                >
                <p v-if="errors.lastName" class="text-red-500 text-sm mt-1">{{ errors.lastName }}</p>
              </div>
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
              <label class="block text-sm font-medium text-secondary-700 mb-2">Пароль</label>
              <div class="relative">
                <input
                  v-model="form.password"
                  :type="showPassword ? 'text' : 'password'"
                  required
                  class="input-field pr-12"
                  :class="{ 'border-red-500': errors.password }"
                  placeholder="Минимум 6 символов"
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

            <div>
              <label class="block text-sm font-medium text-secondary-700 mb-2">Подтвердите пароль</label>
              <div class="relative">
                <input
                  v-model="form.confirmPassword"
                  :type="showConfirmPassword ? 'text' : 'password'"
                  required
                  class="input-field pr-12"
                  :class="{ 'border-red-500': errors.confirmPassword }"
                  placeholder="Повторите пароль"
                >
                <button
                  type="button"
                  @click="showConfirmPassword = !showConfirmPassword"
                  class="absolute right-3 top-1/2 transform -translate-y-1/2 text-secondary-400 hover:text-secondary-600 transition-colors duration-300"
                >
                  {{ showConfirmPassword ? '🙈' : '👁️' }}
                </button>
              </div>
              <p v-if="errors.confirmPassword" class="text-red-500 text-sm mt-1">{{ errors.confirmPassword }}</p>
            </div>

            <div>
              <label class="block text-sm font-medium text-secondary-700 mb-2">Тип аккаунта</label>
              <select v-model="form.accountType" class="input-field">
                <option value="client">Клиент</option>
                <option value="partner">Партнер</option>
                <option value="developer">Разработчик</option>
              </select>
            </div>

            <div class="space-y-3">
              <div class="flex items-center">
                <input
                  v-model="form.agreeTerms"
                  type="checkbox"
                  id="terms"
                  required
                  class="w-4 h-4 text-primary-500 border-secondary-300 rounded focus:ring-primary-500"
                >
                <label for="terms" class="ml-2 text-sm text-secondary-600">
                  Согласен с <a href="#" class="text-primary-500 hover:text-primary-600">условиями использования</a>
                </label>
              </div>
              <div class="flex items-center">
                <input
                  v-model="form.agreePrivacy"
                  type="checkbox"
                  id="privacy"
                  required
                  class="w-4 h-4 text-primary-500 border-secondary-300 rounded focus:ring-primary-500"
                >
                <label for="privacy" class="ml-2 text-sm text-secondary-600">
                  Согласен с <a href="#" class="text-primary-500 hover:text-primary-600">политикой конфиденциальности</a>
                </label>
              </div>
              <div class="flex items-center">
                <input
                  v-model="form.subscribeNewsletter"
                  type="checkbox"
                  id="newsletter"
                  class="w-4 h-4 text-primary-500 border-secondary-300 rounded focus:ring-primary-500"
                >
                <label for="newsletter" class="ml-2 text-sm text-secondary-600">
                  Подписаться на новости и обновления
                </label>
              </div>
            </div>

            <button
              type="submit"
              :disabled="isSubmitting"
              class="w-full btn-primary"
              :class="{ 'opacity-50 cursor-not-allowed': isSubmitting }"
            >
              {{ isSubmitting ? 'Регистрация...' : 'Зарегистрироваться' }}
            </button>
          </form>

          <div class="mt-8 text-center">
            <p class="text-secondary-600">
              Уже есть аккаунт?
              <router-link to="/login" class="text-primary-500 hover:text-primary-600 font-medium transition-colors duration-300">
                Войти
              </router-link>
            </p>
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
        <h3 class="text-2xl font-bold text-secondary-800 mb-2">Регистрация успешна!</h3>
        <p class="text-secondary-600 mb-6">
          Добро пожаловать в WebStudio! Ваш аккаунт создан и готов к использованию.
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
const showConfirmPassword = ref(false)

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  password: '',
  confirmPassword: '',
  accountType: 'client',
  agreeTerms: false,
  agreePrivacy: false,
  subscribeNewsletter: false
})

const errors = reactive({
  firstName: '',
  lastName: '',
  email: '',
  password: '',
  confirmPassword: ''
})

const validateForm = () => {
  // Reset errors
  Object.keys(errors).forEach(key => errors[key] = '')

  let isValid = true

  if (!form.firstName.trim()) {
    errors.firstName = 'Имя обязательно для заполнения'
    isValid = false
  }

  if (!form.lastName.trim()) {
    errors.lastName = 'Фамилия обязательна для заполнения'
    isValid = false
  }

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

  if (!form.confirmPassword.trim()) {
    errors.confirmPassword = 'Подтверждение пароля обязательно'
    isValid = false
  } else if (form.password !== form.confirmPassword) {
    errors.confirmPassword = 'Пароли не совпадают'
    isValid = false
  }

  return isValid
}

const register = async () => {
  if (!validateForm()) return

  isSubmitting.value = true

  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Here you would typically send registration data to your API
    console.log('Registration attempt:', form)
    
    showSuccess.value = true
    
    // Redirect after showing success message
    setTimeout(() => {
      router.push('/login')
    }, 2000)
    
  } catch (error) {
    console.error('Registration error:', error)
    errors.email = 'Пользователь с таким email уже существует'
  } finally {
    isSubmitting.value = false
  }
}
</script>